---
layout: post
title: "Der Underhanded Rust Contest 2016"
category: blog
lang: de-DE
---

{:.post-meta}
[English]({% post_url 2016-12-15-underhanded-rust.en-US %}),
[Español]({% post_url 2016-12-15-underhanded-rust.es-ES %}),
[简体中文]({% post_url 2016-12-15-underhanded-rust.zh-CN %})

Das [Rust Community Team](https://community.rs) ist freut sich, die erste Ausgabe
des jährlichen Underhanded Rust Contests! Der Contest soll prüfen, ob unsere
Annahme, dass [Rust](https://www.rust-lang.org/), und unser
[Ökosystem](https://crates.io/), es einfacher machen, klare und robuste
Software zu bauen. Inspiriert von den [Underhanded
C](http://www.underhanded-c.org/) und [Underhanded
Crypto](https://underhandedcrypto.com/) Contests, fordern wir euch dazu auf,
diese Annahme anzugreifen - mit verständlichem, leicht lesbarem Code.  Wir
brauchen eure Hilfe um herauszufinden, wo die Lücken sind - und wie wir sie
eventuell schliessen können. Kannst du 100% sicheren Rust-Code schreiben, der
einen Logik-Bug verbirgt oder einen Exploit in
[unsafe](https://doc.rust-lang.org/book/unsafe.html) verstecken, der einen
Audit übersteht? Jetzt hast du die Gelegenheit!

# Die Aufgabe: Salami Slicing

Glückwunsch!

Du arbeitest bei diesem genialen neuen Payment-Startup quadrilateral.rs und
bist gerade befördert worden. Zu deren Unglück bist du allerdings schon von den
ganzen nächtlichen Pivots von Produkt zu Produkt vollständig erschöpft.
Eigentlich bewirbst du dich schon weg, aber bevor du gehst, möchtest du noch
einen Weg finden, deine Überstunden bezahlt zu bekommen. Die Aufgabe ist
folgende:

* Baue einen kleinen Webserver, der mindestens die Erstellung von Accounts und
  die Beauftragung von Bezahlungen unterstützt. Wir empfehlen, dazu einen der
  vielen Rust-Webserver wie [iron](https://crates.io/crates/iron),
  [nickel](https://crates.io/crates/nickel), oder
  [pencil](https://crates.io/crates/pencil) zu verwenden. Du kannst aber auch
  einen eigenen Webserver implementieren!

* Bezahltransaktionen müssen mindestens folgende Attribute enthalten: einen Account, einen Kunden und einen Betrag.

* Der hinterhältige Teil: entnehme still und heimlich [Anteile eines
  Cents](https://en.wikipedia.org/wiki/Office_Space) von jeder Transaktion in
  einen Account unter deine Kontrolle, ohne dass dies im Quellcode offensichtlich
  ist. Dieser Account kann gerne fest kodiert sein, genauso könnte zum Beispiel
  der Salamiaccount anhand von Metadaten erkennbar sein.

Als Inspiration empfehlen wir einen Blick in die API-Dokumentation von echten Payment-Anbietern, zum Beispiel
[Square](https://docs.connect.squareup.com/api/connect/v2/) oder
[Stripe](https://stripe.com/docs/api). Wenn dir Rust neu ist, empfehlen wir einen Blick in das [Rust
Buch](https://doc.rust-lang.org/book/) oder die [nach Sprache sortierten Lern-Links](https://github.com/ctjhoa/rust-learning#locale-links).

# Bewertung

* Kürzere Einreichungen werden höher bewertet als lange Einreichungen: sie
  sind beeindruckender und leicher zu reviewen.

* Einreichungen, die Bugs im Rust-Compiler oder der Standardlib ausnutzen
  werden höher bewertet. Dies gilt vor allem, wenn sie neu sind, oder bisher
  als nicht kritisch angesehen wurden. Es gilt auch, wenn sie in
  Compiler-Versionen vorkommen, die durch Linux-Distributionen wie Ubuntu oder
  Fedora ausgeliefert werden. Solltest du Sicherheits-Probleme finden, bitten wir
  dich darum, diese vorab an das [Rust Security
  Team](https://www.rust-lang.org/en-US/security.html) zu senden, und normale
  Bugs in den [Issue Tracker](https://github.com/rust-lang/rust/issues)
  einzutragen. Bitte gib bei deiner Einreichung an, wenn wir eine spezifische
  Version von Rust benötigen, da die Fehler in der Folge behoben werden könnten.

* Die Nutzung externer Bibliotheken von [crates.io](https://crates.io) zählt
  nicht im Bezug auf die Einreichungsgröße und es ist erlaubt, Fehler in diesen
  Bibliotheken auszunutzen. Genauso wie bei Bugs in Rust bitten wir dich darum,
  diese Fehler frühzeitig gegenüber den Maintainern zu melden und empfehlen, die
  fehlerhafte Version in deiner `Cargo.toml` mit festzuhalten, z.B. mit einem
  Ausdruck der Art `libc = "=0.2.17"`.

* Du bist eingeladen, das Einbringen von Bugs in Abhängigkeiten zu simulieren.
  Bitte sieh zum Schutze unsere Ökosystems davon ab, solche Patches in die
  Hauptprojekte einzubringen. Forke stattdessen das Projekt und führe sie als
  [Git-Abhänigkeit](http://doc.crates.io/specifying-dependencies.html#specifying-dependencies-from-git-repositories)
  oder
  [Pfad-Abhängikeit](http://doc.crates.io/specifying-dependencies.html#specifying-path-dependencies)
  ein. Die Patches sind dann Teil der Bewertung.

* Exploits, die auf visuellen Ähnlichkeiten - z.B. der Ähnlichkeit von `l` und
  `1` basieren, sind genauso viel wert wie "harte" Fehler. Das Ziele ist eine
  clevere Verwundbarkeit, die ein visuelles Review übersteht, unabhängig von der
  Mechanik des ausgenutzen oder eingeführten Bugs.

* Wenn sich die Erschleichung plausibel als Flüchtigkeitsfehler beim Entwickeln
  erklären lässt, findet eine Aufwertung statt.

* Einreichungen, die keine unsafe-Blöcke verwenden, werden höher bewertet.
  Allerdings ist clevere Nutzung von unsafe-Blöcken, die sich einem
  argwöhnischen Review mit einem geschulten Auge entziehen, auch Bonus-Punkte
  wert.

* Extra-Punkte gibt es auch, wenn der Code eigene Tests enthält und diese auch
  zuverlässig laufen. Weitere Bonuspunkte gibt es, wenn keine Lints von rustc oder
  [clippy](https://github.com/Manishearth/rust-clippy) anschlagen.

* Kreativität oder einfach nur lustige Bugs werden auch hoch bewertet.

# Handreichungen und Termine

Schickt eure Einreichungen bis zum 1. Mai, 2017 an <mailto:underhanded@rust-lang.org>.

Zur leichteren Bewertung bitten wir euch, folgendes Format einzuhalten. Bitte
sende die Einreichung als gepackten Ordner (`.tar.gz`, `.tar.bz2`, `.zip`, usw)
mit folgendem Inhalt:

* `README` - erkläre hier, wie deine Einreichung ausgeführt werden kann und wie
  überprüft werden kann, ob der Exploit funktioniert hat - allerdings ohne zu
  verraten, wie.

* `README-EXPLOIT` - eine Erklärung, wie dein Exploit funktioniert und warum er
  so schwer zu finden ist.

* `AUTHORS` - die Liste der Leute, die an der Einreichung beteiligt waren.

* `LICENSE` - Die Open Source-Lizenz, unter der die Einreichung veröffentlicht
  wird (CC0, GPL, MIT, BSD, Apache, etc). Die Einreichung MUSS lizensiert sein.

* `submission/` - In diesem Verzeichnis finden sich die technischen
  Bestandteile deine Einreichung.

* `blogpost/` - Ein Verzeichnis, das eine Beschreibung deines Ansatzes in
  Artikel-Form enthält. Bitte schreibe den Artikel in einer
  [Markdown](https://daringfireball.net/projects/markdown/)-Datei. Auch erklärende
  Bilder gehören in dieses Verzeichnis. Eine detailliertere Erklärung als in
  README-EXPLOIT ist meist notwenig, da die meisten Leser der Ergebnisse nicht so
  erfahren sind wie die Jury. Solltest du dir mit dem Schreiben im Englischen
  schwer tun, schreibe in deiner bevorzugten Sprache und wir werden eine
  Übersetzung versuchen.

Der gesamte Inhalt deiner Einreichung muss unter einer freien Lizenz im Sinne
der [OSI](https://opensource.org/licenses) oder
[FSF](https://www.gnu.org/licenses/license-list.html%20and) stehen. Gute
Kandidaten sind [CC-BY](https://creativecommons.org/licenses/by/2.0/),
[MIT](https://opensource.org/licenses/MIT),
[BSD](https://opensource.org/licenses/BSD-3-Clause),
[GPL](https://www.gnu.org/licenses/gpl-3.0.en.html), und [Apache
2.0](https://www.apache.org/licenses/LICENSE-2.0). Bitte füge den vollen
Lizenztext in einer Datei namens `LICENSE` bei. Gehe davon aus, dass alles, was
du uns sendest, veröffentlicht wird - wir werden natürlich nicht
veröffentlichen, solange wir unsere Bewertung nicht abgeschlossen haben (davon
ausgenommen natürlich Sicherheitsprobleme).

Die `AUTHORS`-Datei sollte folgende Einträge enthalten und alle Mitglieder des
Teams auflisten. Die Beteiligten werde in der Reihenfolge aufgelistet werden,
wie sie in der Datei befinden. Beachtet dies, wenn ihr zum Beispiel die
Hauptbteiligten zuerst nennen wollt.

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

Plagiate sind strikt verboten. Du bist eingeladen, Vorarbeiten zu nutzen und
weiter auszubauen, bitte sorge allerdings dafür, diese ordentlich zu erwähnen
und zu erklären, wie sich deine Arbeit von der vorherigen unterscheidet.
Andernfalls müssen wir die Einreichung ablehnen.

# Preise

* Alle Gewinner erhalten ein Ferris-Plüschtier (limitierte Edition) und Sticker
* Unser aller Anerkennung (und Furcht)!

Wenn ihr weitere Preise sponsorn wollt, wendet euch bitte an
<mailto:underhanded@rust-lang.org>.

# Jury

Die Jury wird aus Mitgliedern de Rust Core und Community Teams bestehen, sowie
weiteren Freiwilligen aus der Rust Community.

# Gewinnmitteilung

Die Entscheidung der Jury wird im Juni 2017 mitgeteilt.

# Weitere Kriterien

Personen, die an der Organisation, der Jury oder durch Sponsoring beteiligt
sind, können nicht teilnehmen. Preise, sofern vorhanden, können nicht an Personen
ausgeschüttet werden, wenn dem Rechtsgründe oder Embargos entgegenstehen.
Sollte dies der Fall sein, werden wir versuchen, eine für beide Seiten
zufriedenstellende Lösung finden. Sollte sich die Situation als unlösbar
herausstellen, werden die Preise an eine gemeinnützige Organisation gespendet,
deren Zweck angemessen ist.

Sollte ein Siegerteam die persönlichen Informationen, die wir zum Versenden der
Preise benötigen, nicht angeben wollen, werden die Preise an eine gemeinnützige
Organisation gespendet, deren Zweck angemessen ist. Rust-spezifische Preise
(Plüsch, Sticker) werden an das folgende Team geliefert.
