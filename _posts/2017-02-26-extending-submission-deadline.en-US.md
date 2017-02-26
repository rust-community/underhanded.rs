---
layout: post
title: "Extending the Underhanded Submission Deadline"
category: blog
lang: en-US
---

Hello Underhanded Rustlers!  The [Rust Community Team][rust_community_team] has
extended the submission deadline for the Underhanded Rust Contest to March 31,
2017.  We wanted to help give people new to Rust a little more time to get
ramped up on the language.  As part of this, we have developed a few new
resources to get you on your way.

First, we have created a simple example we're calling [quad-bank][quad_bank].
It builds out a simple payment processor using a number of popular Rust
libraries, like the SQL ORM [Diesel][diesel], and the web frameworks
[Iron][iron] and [Rocket][rocket]. It also has contains what's probably the
simplest exploit possible, zero authentication and no bounds checking on
transfers. Feel free to lift any code from this project.

Second, we have created a dedicated IRC channel for the contest
[#underhanded-rust][underhanded_rust_irc] where we can help you get started,
address any problems, and answer any questions about the contest.

Third, we've started collecting relevant [posts][resisting_underhandedness]
from around our community about underhandedness in Rust, and the various things
we can do to resist them.

[rust_community_team]: https://community.rs
[diesel]: http://diesel.rs
[iron]: http://ironframework.io/
[rocket]: https://rocket.rs/
[quad_bank]: https://github.com/erickt/quad-bank
[underhanded_rust_irc]: https://client00.chat.mibbit.com/?server=irc.mozilla.org&channel=%23underhanded-rust
[resisting_underhandedness]: https://github.com/rust-community/underhanded.rs/wiki/Resisting-Underhandedness

# Questions from the community

We've had a few variations of the same question:

* Does my submission have to steal fractions of a penny over multiple requests,
  or can it steal in one large transaction?
* Can I directly attack another account rather than shave pennies off each
  transaction?
* Can I directly target account to account transfers instead of capturing some
  pennies off each transaction?

The answer to all of these is yes, this is fine. We are pretty open to how you
want to get rich with these attacks. The narrative we [setup][announcement] is
about getting you in the spirit of the game, but we're more interested in your
underhandness than staying perfectly in our story.

---

* Can I disable ASLR or other safety mechanisms?

Yes, that's fine, but you might lose some points. However, if you can come up
with a plausible justification why disabled these mechanisms, you'll gain
points. Because we're a systems language, there will always be situations where
safety valves will need to be turned off, but our community needs to make sure
we have good explanations of when this is actually needed, and when it's highly
suspicious.

---

* I wonder if simply being vulnerable to SQL injection counts.

Yes, we'd love to see classic attacks like this!

---

If you have any other questions, please feel free to either ask on
<mailto:underhanded@rust-lang.org>, or on our IRC channels [#rust-community] or
[#underhanded-rust].

Have fun causing trouble!

[announcement]: https://underhanded.rs/blog/2016/12/15/underhanded-rust.en-US.html
[#rust-community]: https://client00.chat.mibbit.com/?server=irc.mozilla.org&channel=%23rust-community
[#underhanded-rust]: https://client00.chat.mibbit.com/?server=irc.mozilla.org&channel=%23underhanded-rust
