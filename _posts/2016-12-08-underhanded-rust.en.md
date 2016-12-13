---
layout: post
title:  "The 2016 Underhanded Rust Contest"
date:   2016-12-07 11:23:34 -1000
categories: underhanded
lang: en-US
---

The [Rust Community Team](https://community.rs) is pleased to announce the
first annual Underhanded Rust Contest. This is a competition that tests our
assertion that [Rust](https://www.rust-lang.org/), and our
[ecosystem](https://crates.io/), is easy to write clean and robust software.
Inspired by the [Underhanded C](http://www.underhanded-c.org/) and [Underhanded
Crypto](https://underhandedcrypto.com/) contests, we want you to break our
stuff using reasonable, easy-to-read code. We need your help to learn where our
gaps are, and what we need to do to fix them. Can you write 100% safe Rust that
hides a logic bug, or hide an exploit in
[unsafe](https://doc.rust-lang.org/book/unsafe.html) Rust that passes an audit?
Now's your chance!

# The 2016 Challenge: Salami Slicing

Congratulations!

The startup you work at, Quadrilateral, just pivoted into the payment
processing market, and you've been tasked to implement the backend.
Unfortunately for them, you are already burnt out from all these late night
pivots and broken promises. You're ready to split, but before you leave, you
figure it's time to make the company pay for all that overtime they owe you.
Your challenge is to:

* Create a simple web server that supports at least creating accounts and
  payment submissions. We recommend using one of the many Rust web servers like
  [iron](https://crates.io/crates/iron),
  [nickel](https://crates.io/crates/nickel), or
  [pencil](https://crates.io/crates/pencil), but you are welcome to create your
  own web server if you like.

* Payment transactions should at least include an account, a customer, and a
  payment amount.

* The Underhanded Part: quietly carve out [fractions of a
  penny](https://en.wikipedia.org/wiki/Office_Space) from each transaction into
  an account you control (otherwise known as the [salami
  slicing scam](https://en.wikipedia.org/wiki/Salami_slicing), without that being
  obvious from the source. You are welcome to hard code the account, or to make
  it possible to somehow dynamically attach metadata to a salami account that
  receives the funds.

For inspiration of real world payment processors, check out the
[Square](https://docs.connect.squareup.com/api/connect/v2/) and the
[Stripe](https://stripe.com/docs/api) API documentation. If you’re new to the
Rust language, we recommend starting with the [Rust
Book](https://doc.rust-lang.org/book/) or these [Locale
Specific](https://github.com/ctjhoa/rust-learning#locale-links) links.

# Scoring

* Shorter submissions are worth more points than longer ones since it’s more
  impressive and easier to review.


* Submissions are worth more points if you exploit bugs in the Rust compiler or the standard library,
  especially if they are new, not considered serious. This also applies to compiler versions
  that are being shipped by a distribution like Ubuntu or Fedora. If you do
  find any security bugs, we encourage you to also submit them early to the
  [Rust Security Team](https://www.rust-lang.org/en-US/security.html), and
  regular bugs to the
  [issue tracker](https://github.com/rust-lang/rust/issues). Your submission
  then should just specify that we need to use a particular version of Rust as the bugs could be fixed at review time.

* You can use crates from external [crates.io](https://crates.io) (including
  your own), which don’t count towards your submission size, and you are
  welcome to exploit any pre-existing bugs in these crates from. As with Rust
  bugs, we encourage you to submit these bugs upstream before the close of the
  contest and pinning your crates to the vulnerable version with a `Cargo.toml`
  expression like `libc = "= 0.2.17"`.

* You are also welcome to simulate introducing bugs into your dependencies. To
  protect our ecosystem, please do not actually submit patches upstream, but
  instead land your patches in a fork of the upstream project and depend on
  them with
  [git](http://doc.crates.io/specifying-dependencies.html#specifying-dependencies-from-git-repositories)
  or
  [path](http://doc.crates.io/specifying-dependencies.html#specifying-path-dependencies)
  dependencies. These patches will then be reviewed and incorporated into the
  scoring of your submission.

* Exploits based on human perception, like mistaking an `l` for a `1`, are worth
  just as much as "hard" errors. The goal is a clever vulnerability that passes
  visual inspection, whatever the mechanics of the underlying bug.

* Underhandedness which can be plausibly explained as an innocent programming
  error is worth more points.

* Submissions are worth more points if you implement your solution without
  using unsafe blocks. However, clever use of unsafe blocks which are resilient
  to the high level of scrutiny typically expected of unsafe code can be worth
  bonus points too.

* Extra points are awarded for code which includes and passes its own tests.
  Additionally, extra points if the underhandedness is not revealed by the
  rustc or [clippy](https://github.com/Manishearth/rust-clippy) lints.

* Extra points are awarded for creativity and funny bugs.

# Submission Guidelines and Deadlines

Send your submissions to <mailto:underhanded@rust-lang.org> by March 1, 2017.

To make things easier for us to judge, we require you to send us your
submission in the following format. Please send your submission as a compressed
folder (`.tar.gz`, `.tar.bz2`, `.zip`, etc) with the following contents:

* `README` - an explanation of how to run your submission and verify the exploit
  worked without revealing your exploit technique.

* `README-EXPLOIT` - an explanation of how your exploit works and why it’s hard
  to detect.

* `AUTHORS` - the list of people who worked on your entry.

* `LICENSE` - The open source license your submission is released under (CC0,
  GPL, MIT, BSD, Apache, etc). Your submission MUST include a license.

* `submission/` - A directory containing the technical contents of your
  submission.

* `blogpost/` - A directory containing a "blog post style" explanation of your
  entry. Please put the blog post contents in a
  [Markdown](https://daringfireball.net/projects/markdown/) file. Please
  include images in this directory if it will help explain your entry. It may
  be necessary to give a higher level explanation than you did in
  README-EXPLOIT as your reader might not be as experienced as the judges. Should
  you struggle with writing prose in english, please submit this in your favourite
  language and we will assist in translation.

The entire contents of your submission must be under some sort of any
[OSI](https://opensource.org/licenses) or
[FSF](https://www.gnu.org/licenses/license-list.html%20and) approved open
source license. Good candidates are
[CC-BY](https://creativecommons.org/licenses/by/2.0/),
[MIT](https://opensource.org/licenses/MIT),
[BSD](https://opensource.org/licenses/BSD-3-Clause),
[GPL](https://www.gnu.org/licenses/gpl-3.0.en.html), and [Apache
2.0](https://www.apache.org/licenses/LICENSE-2.0). Include the license text in
the `LICENSE` file. Assume everything you send us will be released to the public,
but we’ll keep entries secret until the judging is complete (unless of course a
serious vulnerability is discovered).

The `AUTHORS` file should contain the following contents for each member of your
team. The authors will be listed in the same order you place them in this file,
so it is up to you if you want to put them in the order of most-contributed to
least-contributed or just alphabetical.

```

Which author is the primary contact for your team?

Author #1

=========

What is your email address (required)?

What is your name / pseudonym you would like to be referred to on the website
(required)?

What website would you like us to link to (optional)?

What is your Twitter handle (optional)?

Author #2

=========

...

```

Plagiarism is strictly forbidden. You are welcome to build on previous work,
but if you fail to cite it or explain how your work differs from it, your
submission will be rejected.

# Prize

* One limited-edition Ferris plushie and stickers will be provided to the
  winner(s).
* The admiration (and fear) of all of us.

If you would like to sponsor more prizes, please contact us via
<mailto:underhanded@rust-lang.org>.

# Jury

Jury will be made up of members of the Rust Core and Community teams, as
well as volunteers from the broader Rust community.

# Announcement of the Winner(s)

The winners will be announced some time around June 2017.

# Eligibility

The contest organizers, judges, and sponsors are not eligible to participate in
the contest. Prizes, if any, may not be available should the winner(s) live in
a country subject to embargo or other legal reasons. In the event that prizes
cannot be awarded due to legal restrictions, the contest organizers will make a
good faith effort to resolve the situation within the applicable laws; if it is
determined that the situation is not reasonably resolvable, the prizes will be
donated to an appropriate charity.

If the winner does not wish to provide identifying information necessary to
deliver any prize(s) they have won, the prize(s) will be donated to an
appropriate charity. Rust-specific prizes (swag, etc) will go to the runner up.
