---
layout: post
title: "2016 Rust黑手大赛"
categories: blog
lang: zh-CN
---

{:.post-meta}
[Deutsche]({% post_url 2016-12-15-underhanded-rust.de-DE %}),
[English]({% post_url 2016-12-15-underhanded-rust.en-US %}),
[Español]({% post_url 2016-12-15-underhanded-rust.es-ES %}),

[Rust社区团队](https://community.rs)很高兴地宣布首届“Rust黑手大赛”（Underhanded Rust Contest）。这场比赛主旨是为了测试[Rust](https://www.rust-lang.org/)的主张和我们的[生态系统](https://crates.io/)，用它可以很容易地编写干净健壮的软件。秉承“C黑手”（[Underhanded C](http://www.underhanded-c.org/) ）和 “Crypto黑手”（[Underhanded
Crypto](https://underhandedcrypto.com/) ）比赛的理念，我们希望您使用合理、可读的代码来打破一切。我们需要您的帮助来了解缺陷在哪里以及要修复它们需要做些什么。您是否可以编写一个100%安全但又隐藏逻辑bug，或者，仪仗[unsafe](https://doc.rust-lang.org/book/unsafe.html)来通过编译器审计但又隐藏了漏洞的Rust代码？现在，展示您能力的机会来了！


# 2016年挑战：腊肠切片（Salami Slicing）

恭喜!

您工作的创业公司Quadrilateral刚刚进军支付市场，您的职责是负责后端任务的实现。
但（对他们来说）不幸的是，您已经厌倦了他们这种两眼一抹黑的转型和无法兑现的承诺。
您已经决定了退出，但是在离开之前，您认为是时候让公司支付他们欠您的所有加班费了。

您的挑战是：

* 创建一个简单的web服务器，至少支持创建帐号和支付提交。我们建议选择使用社区的众多Rust Web服务器之一，比如[iron](https://crates.io/crates/iron),
[nickel](https://crates.io/crates/nickel), 或
[pencil](https://crates.io/crates/pencil)，当然如果您愿意的话也欢迎您创建您自己的Web服务器。

* 支付交易应该至少包含账户、客户以及支付金额。

* 黑手部分：从每笔交易中悄悄的分出一些零头（[来自于电影: Office Space](https://en.wikipedia.org/wiki/Office_Space)）到您控制的账户中（也叫意大利腊肠骗局（[salami slicing
scam](https://en.wikipedia.org/wiki/Salami_slicing)）），而交易金额没有明显的影响。欢迎您硬编码到帐号中，或者是以某种动态的方式将元数据附加到腊肠帐号中用来接收资金。

可以通过查阅[Square](https://docs.connect.squareup.com/api/connect/v2/) 和
[Stripe](https://stripe.com/docs/api) API文档找点灵感。如果您是Rust语言新手，我们建议您从[Rust
Book](https://doc.rust-lang.org/book/) 或 [特定语言的资讯](https://github.com/ctjhoa/rust-learning#locale-links)开始。

# 评分标准

* 代码越短越容易加分，因为它更优雅更容易评审。

* 如果您能利用Rust编译器或标准库中的Bug就更容易加分，尤其当它们是新的并且不被认为是严重的错误或bug。同样适用于Ubuntu 和 Fedora这样的发行版中提供的编译器版本。如果您发现任意安全bug，我们建议您尽早将其提交给[Rust安全团队](https://www.rust-lang.org/en-US/security.html)，并经常向[issue tracker](https://github.com/rust-lang/rust/issues)提交bug。您的提交应该指定我们需要使用的Rust的特定版本，以便Bug可以在评审期间被修复。

* 您可以使用来自于[crates.io](https://crates.io)（包括您自己写的）的包，这部分提交尺寸不会计入评分中，欢迎您利用任何预先存在错误的这些包。与Rust Bug一样，我们鼓励您在比赛结束前提交这些错误，并使用`Cargo.toml`（比如 `libc = "= 0.2.17"`）将您的包锁定到易受攻击的版本。

* 您也可以在您的依赖中假装引入bug。为了保护我们的生态系统，请不要真正的向上游提交补丁，而是将您的补丁挂在上游项目的一个分支下，并使用[git](http://doc.crates.io/specifying-dependencies.html#specifying-dependencies-from-git-repositories)
或
[path](http://doc.crates.io/specifying-dependencies.html#specifying-path-dependencies)依赖它们。这些补丁将会被审查并且纳入评分中。

* 基于人类感知的漏洞，比如把`l` 错看为 `1`，和硬性的错误评分标准一样。不管底层bug的工作机制，只要能通过视觉的审查，就算合法。

* 可以被合理解释为无害程序错误的“黑手”将会得到更多的分。

* 如果您的实现没有使用unsafe块，那么将获得更多的分。然而，聪明的使用unsafe块，通过通常对不安全代码的预期来提升审查的水准，是值得获得更多的分值奖励的。

* 包含并通过自己的测试代码将获得额外的积分。此外，如果没有把“黑手”暴露给rustc或 [clippy](https://github.com/Manishearth/rust-clippy) lints，也会获得额外积分。

* 富有创造力和有趣的“黑手”将获得额外的积分奖励。

# 提交指南与截止日期

在2017年3月1日之前把您的提交程序发送至<mailto:underhanded@rust-lang.org>。

为了方便我们评判，我们需要您按下面格式来发送您提交的程序。请将您的提交压缩为(`.tar.gz`, `.tar.bz2`, `.zip`, 等)压缩文件，并包含下面内容：

* `README` - 用于解释您提交的程序如何运行，以及在不暴露漏洞技术的情况下如何验证漏洞是否工作

* `README-EXPLOIT` - 用于解释您的漏洞工作机制以及为什么它难于被检测到。

* `AUTHORS` - 参与这份提交程序的参与者名单。

* `LICENSE` - 您提交程序的开源许可证是在 (CC0,
  GPL, MIT, BSD, Apache, 等)下发布的。您的提交必须包含一个许可证。

* `submission/` - 此目录包含您提交的所有代码文件。

您提交的整个内容必须是某种[OSI](https://opensource.org/licenses)或[FSF](https://www.gnu.org/licenses/license-list.html%20and)批准的开源许可证。 好的选择是[CC-BY](https://creativecommons.org/licenses/by/2.0/),
[MIT](https://opensource.org/licenses/MIT),
[BSD](https://opensource.org/licenses/BSD-3-Clause),
[GPL](https://www.gnu.org/licenses/gpl-3.0.en.html), 和 [Apache
2.0](https://www.apache.org/licenses/LICENSE-2.0)。 将许可证文本包含在`LICENSE` 文件中。 我们假设您发送给我们的所有内容都将公开发布，但在评审完成（除非发现严重的漏洞）之前，我们会为您保密。

`AUTHORS` 文件应为您团队中每个成员包含以下内容。作者们将按照放置在此文件中的顺序列出，因此，可以由您来决定是否将他们按照最少贡献的顺序或仅按字母或拼音顺序排列。


```

哪位作者是您团队的主要联系人？

作者 #1

=========

您的email地址是什么(必需)?

您想在网站上显示的名字或化名是什么（必需）？

您想要我们链接到哪个网站（可选）？

您的Twitter用户名是什么（可选）?

作者 #2

=========

...

```

严格禁止剽窃。 欢迎您参考之前的成果，但是如果您没有引用它或者解释您的工作和它有什么不同，您的提交将会被拒绝。

# 奖品

* 一个限量版的Ferris绒毛玩具（Ferris是Rust官方动物logo）和贴纸。
* 我们所有人的钦佩（和恐惧）。

如果您想赞助更多的奖品，请通过<mailto:underhanded@rust-lang.org>与我们联系。

# 评审团

评审团将由Rust核心团队和社区团队组成，以及广大的Rust社区志愿者们。

# 优胜者公告

获奖者将在2017年6月左右宣布。

# 领奖资格

比赛组织者、评审官以及赞助商不符合参赛资格。奖品可能无法颁发给居住于有禁运令或其他法律限制国家的获奖者。对于因为法律原因不能颁发的情况，比赛组织者将在法律允许的范围内尽最大努力来解决问题。如果是不能合理解决的情况，奖品将会捐赠给慈善机构。

如果获奖者不希望提供用于寄送奖品的必要身份信息，则奖品会被捐赠给慈善机构。第一名之后的获奖者将会获得具体Rust特色的奖品（[比如贴纸、T恤](https://gist.github.com/brson/169768d19359fcac631c0bf7998acca8)）。
