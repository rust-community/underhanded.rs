---
layout: post
title: "Mitigating Underhandedness: Fuzzing Your Code"
category: blog
lang: en-US
---

_Note: This is reposted with permission from [Manish Goregaokar]._

 [Manish Goregaokar]: http://manishearth.github.io/blog/2017/03/02/mitigating-underhandedness-fuzzing-your-code/

---

The [submission deadline for the Underhanded Rust competition has been extended][submit], so
let's talk more about how to keep your code working and free from bugs/underhandedness!

[Previously, we talked about Clippy][post-prev].


 [submit]: https://underhanded.rs/blog/2017/02/28/extending-submission-deadline.en-US.html
 [post-prev]: http://manishearth.github.io/blog/2017/01/21/mitigating-underhandedness-clippy/

Now, really, underhanded bugs are just another form of bug. And how do we find bugs? We test!

We write unit tests. We run the code under Valgrind, ASan, MSan, UBSan, TSan, and any other sanitizer
we can get our hands on. Tests tests tests. More tests. Tests.

But, there's a problem here. You need to write _test cases_ to make this work. These are inputs
fed to your code after which you check whatever invariants your code has. There's
no guarantee that the test cases you write will exercise all the code paths in your
program. This applies for sanitizers too, sanitizers are limited to testing the code paths
that your test cases hit.

Of course, you can use code coverage tools to ensure that all these code paths will be hit.
However, there's a conflict here -- your code will have many code paths that are
_not supposed to be hit ever_. Things like redundant bounds checks, null checks, etc.
In Rust programs such code paths generally use panics.

Now, these code paths are never _supposed_ to be hit, so they'll never show up in your
code coverage. But you don't have a guarantee that they can never be hit, short
of formally verifying your program. The only solution here is writing more test cases.

Aside from that, even ignoring those code paths, you still need to manually write
test cases for everything. For each possible code path in your code, if you want to
be sure.

Who wants to manually write a million test cases?

![ain't nobody got time for that]({{ site.url }}/assets/memes/aint-nobody.jpg){: .center-image width="400" }

![If someone would write my test cases for me, that'd be great]({{ site.url }}/assets/memes/that-would-be-great.jpg){: .center-image width="400" }

Enter fuzzing. What fuzzing will do is feed your program random inputs, carefully watching the
codepaths being taken, and try to massage the inputs so that new, interesting (usually crashy)
codepaths are taken. You write tests for the fuzzer such that they can accept arbitrary input, and
the fuzzer will find cases where they crash or panic.

One of the most popular fuzzers out there is [AFL][afl], which takes a binary and feeds it random
input. Rust [has a library that you can use for running AFL][afl.rs], however it currently needs
to be run via a Docker image or needs a recompilation of rustc, since it adds a custom LLVM pass.
We're working on making this step unnecessary.

However, as of a few weeks ago, we now have bindings for [libFuzzer], which uses existing
instrumentation options built in to LLVM itself! libFuzzer works a bit differently; instead
of giving it a binary, you write a function in a special way and give it a library containing
that function, which it turns into a fuzzer binary. This is faster, since the fuzzer lives
inside the binary itself and it doesn't need to execute a new program each time.

Using libFuzzer in Rust is easy. Install [`cargo-fuzz`][cargo-fuzz]:

 [afl]: http://lcamtuf.coredump.cx/afl/
 [afl.rs]: https://github.com/rust-fuzz/afl.rs
 [libFuzzer]: http://llvm.org/docs/LibFuzzer.html
 [cargo-fuzz]: https://github.com/rust-fuzz/cargo-fuzz

```sh
$ cargo install cargo-fuzz
```

Now, within your crate, initialize the fuzz setup:

```sh
$ cargo fuzz init
```

This will create a fuzzing crate in `fuzz/`, with a single "fuzz target", `fuzzer_script_1`.
You can add more such targets with `cargo fuzz add name_of_target`. Fuzz targets are small libraries
with a single function in them; the function that will be called over and over again by the fuzzer.
It is up to you to fill in the body of this function, such that the program will crash or panic
if and only if something goes wrong.

For example, for the `unicode-segmentation` crate, [one of the fuzz targets I wrote][unifuzz] just
takes the string, splits it by grapheme and word boundaries, recombines it, and then asserts that
the new string is the same.

```rust
pub extern fn go(data: &[u8]) {
    // we only deal with unicode input
    // bail early, *without panicking* if the input isn't utf8
    if let Ok(s) = str::from_utf8(data) {
        // split into graphemes, recollect
        let result = UnicodeSegmentation::graphemes(s, true).flat_map(|s| s.chars()).collect::<String>();
        // recollected string should be the same as the input, panic if not
        assert_eq!(s, result);

        // split into words, recollect
        let result = s.split_word_bounds().flat_map(|s| s.chars()).collect::<String>();
        // recollected string should be the same as the input, panic if not
        assert_eq!(s, result);
    }
}
```

The other targets ensure that the forward and reverse word/grapheme
iterators produce the same results. They all take the byte slice input, attempt to convert to UTF8
(silently failing  -- NOT panicking -- if not possible), and then use the string as an input
testcase.

Now, these targets will panic if the test fails, and the fuzzer will try and force that panic to
happen. But also, these targets put together exercise most of the API surface of the crate, so
the fuzzer may also find panics (or even segmentation faults!) in the crate itself. For example,
the [fuzz target for rust-url][urlfuzz] doesn't itself assert; all it does is try to parse the given
string. The fuzzer will try to get the URL parser to panic.

To run a fuzz script:

```sh
$ cargo fuzz run fuzzer_script_1
```

This will start the fuzzer, running until it finds a crash or panic. It may also
find other things like inputs which make the code abnormally slow.

Fuzzing can find some interesting bugs. For example, the unicode-segmentation
fuzzers found [this bug][unibug], where an emoji followed by _two_ skin tone modifiers
isn't handled correctly. We'd probably never have been able to come up with this testcase on our
own. But the fuzzer could find it!

The Rust Cap'n Proto crate ran cargo-fuzz and found [a whole ton of bugs][capnpbug]. There
are more such examples [in the trophy case][trophy] (be sure to add any of your own findings
to the trophy case, too!)


cargo-fuzz is relatively new, so the API and behavior may still be tweaked a bit before 1.0.
But you can start taking it for a spin now, and finding bugs!


 [unifuzz]: https://github.com/Manishearth/unicode-segmentation/blob/99b3636ef6b4d96c05644403c1c2eccba2c5f5db/fuzz/fuzzers/equality.rs
 [urlfuzz]: https://github.com/servo/rust-url/blob/3e5541e51e02d8acb10a6ea8ab174ba1bc23ce41/fuzz/fuzzers/parse.rs#L10
 [unibug]: https://github.com/unicode-rs/unicode-segmentation/issues/19
 [capnpbug]: https://dwrensha.github.io/capnproto-rust/2017/02/27/cargo-fuzz.html
 [trophy]: https://github.com/rust-fuzz/cargo-fuzz#trophy-case
