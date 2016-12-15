---
layout: post
title:  "The 2016 Underhanded Rust Contest"
date:   2016-12-07 11:23:34 -1000
categories: underhanded
lang: en-US
---

[Команда связей с сообществом Rust](https://community.rs) рада сообщить о первом
ежегодном соревновании Underhanded Rust. Это соревнование должно проверить наше 
предположение о готовности языка [Rust](https://www.rust-lang.org/) и его 
[экосистемы](https://crates.io/) к написанию легко читаемого и надежного кода.
Воодушевившись примерами [Underhanded C](http://www.underhanded-c.org/) и 
[Underhanded Crypto](https://underhandedcrypto.com/), мы хотим, чтобы вы 
заставили Rust работать неправильно, используя лёгкий для чтения код, к
которому сложно придраться. Нам нужна ваша помощь в поиске брешей в языке
и способов их исправления. Сможете ли вы написать стопроцентно безопасный
код, скрывающий логическую ошибку, или так спрятать эксплойт в 
[unsafe](https://doc.rust-lang.org/book/unsafe.html) коде, чтобы он прошел
аудит? Попробуйте это сделать!

# Проблема 2016: нарезать колбасу

Поздравляем!

Стартап "Четырехугольник", в котором вы работаете, вышел на рынок
обработки платежей, и вам поручено написать бэкенд. Им не повезло.
Вам окончательно надоела неоплачиваемая работа по вечерам и невыполненные 
обещания. Вы готовы уволиться, но, перед тем как уходить, вы решили 
заставить компанию заплатить за все. Ваша задача:

* Создайте простой веб-сервер, поддерживающий создание счетов и обработку
  платежей. Мы рекомендуем использовать один из многих веб-серверов
  написанных на Rust, например
[iron](https://crates.io/crates/iron),
[nickel](https://crates.io/crates/nickel) или
[pencil](https://crates.io/crates/pencil), но вы можете написать и свой.

* Платежная транзакция должна по меньшей мере включать номер счета, 
  контрагента и сумму платежа.

* Предмет конкурса: осторожно отделите 
  [доли копейки](https://ru.wikipedia.org/wiki/%D0%9E%D1%84%D0%B8%D1%81%D0%BD%D0%BE%D0%B5_%D0%BF%D1%80%D0%BE%D1%81%D1%82%D1%80%D0%B0%D0%BD%D1%81%D1%82%D0%B2%D0%BE) 
от каждой транзакции, и переведите их на свой счет (эта атака так же
известна как [salami slicing 
scam](https://en.wikipedia.org/wiki/Salami_slicing) ).
Сделайте это так, чтобы по исходному коду сложно было догадаться о 
происходящем. Вы можете вписать номер своего счета в код, или
каким-то образом динамически добавить метаданные к счету,
предназначенному для получения "отрезанных" сумм.

Посмотрите документацию на API 
[Square](https://docs.connect.squareup.com/api/connect/v2/) и
[Stripe](https://stripe.com/docs/api), чтобы получить представление
о том, что используется для реальной обработки платежей.
Если вам не знаком язык Rust, мы рекомендуем начать с книги [Язык 
программирования Rust](http://rurust.github.io/rust_book_ru/src/INTRODUCTION.html) 
или [других переводов](https://github.com/ctjhoa/rust-learning#locale-links).

# Scoring

* Shorter submissions are worth more points than longer ones since it’s more
  impressive and easier to review.


* Submissions are worth more points if you exploit bugs in the Rust compiler or
  the standard library, especially if they are new, not considered serious.
This also applies to compiler versions that are being shipped by a distribution
like Ubuntu or Fedora. If you do find any security bugs, we encourage you to
also submit them early to the [Rust Security
Team](https://www.rust-lang.org/en-US/security.html), and regular bugs to the
[issue tracker](https://github.com/rust-lang/rust/issues). Your submission then
should just specify that we need to use a particular version of Rust as the
bugs could be fixed at review time.

* You can use crates from external [crates.io](https://crates.io) (including
  your own), which don’t count towards your submission size, and you are
welcome to exploit any pre-existing bugs in these crates from. As with Rust
bugs, we encourage you to submit these bugs upstream before the close of the
contest and pinning your crates to the vulnerable version with a `Cargo.toml`
expression like `libc = "= 0.2.17"`.

* You are also welcome to simulate introducing bugs into your dependencies. To
  protect our ecosystem, please do not actually submit patches upstream, but
instead land your patches in a fork of the upstream project and depend on them
with
[git](http://doc.crates.io/specifying-dependencies.html#specifying-dependencies-from-git-repositories)
or
[path](http://doc.crates.io/specifying-dependencies.html#specifying-path-dependencies)
dependencies. These patches will then be reviewed and incorporated into the
scoring of your submission.

* Exploits based on human perception, like mistaking an `l` for a `1`, are
  worth just as much as "hard" errors. The goal is a clever vulnerability that
  passes visual inspection, whatever the mechanics of the underlying bug.

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

* `README` - an explanation of how to run your submission and verify the
  exploit worked without revealing your exploit technique.

* `README-EXPLOIT` - an explanation of how your exploit works and why it’s hard
  to detect.

* `AUTHORS` - the list of people who worked on your entry.

* `LICENSE` - The open source license your submission is released under (CC0,
  GPL, MIT, BSD, Apache, etc). Your submission MUST include a license.

* `submission/` - A directory containing the technical contents of your
  submission.

* `blogpost/` - A directory containing a "blog post style" explanation of your
  entry. Please put the blog post contents in a
  [Markdown](https://daringfireball.net/projects/markdown/) file. Please include
  images in this directory if it will help explain your entry. It may be
  necessary to give a higher level explanation than you did in README-EXPLOIT as
  your reader might not be as experienced as the judges. Should you struggle with
  writing prose in english, please submit this in your favourite language and we
  will assist in translation.

The entire contents of your submission must be under some sort of any
[OSI](https://opensource.org/licenses) or
[FSF](https://www.gnu.org/licenses/license-list.html%20and) approved open
source license. Good candidates are
[CC-BY](https://creativecommons.org/licenses/by/2.0/),
[MIT](https://opensource.org/licenses/MIT),
[BSD](https://opensource.org/licenses/BSD-3-Clause),
[GPL](https://www.gnu.org/licenses/gpl-3.0.en.html), and [Apache
2.0](https://www.apache.org/licenses/LICENSE-2.0). Include the license text in
the `LICENSE` file. Assume everything you send us will be released to the
public, but we’ll keep entries secret until the judging is complete (unless of
course a serious vulnerability is discovered).

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
