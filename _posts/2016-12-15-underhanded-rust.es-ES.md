---
layout: post
title: "El Underhanded Rust Contest 2016"
date: 2016-12-07 11:23:34 -1000
categories: blog/es-ES
lang: es-ES
---

El [Rust Community Team](https://community.rs) está encantado de anunciar el
primer Underhanded Rust Contest. Esta es una competición que pone a prueba
nuestra afirmación de que con [Rust](https://www.rust-lang.org/), y nuestro
[ecosistema](https://crates.io/) es sencillo escribir software limpio y robusto.

Inspirado por los concursos [Underhanded C](http://www.underhanded-c.org/)
y [Underhanded Crypto](https://underhandedcrypto.com/), queremos que rompas
cosas usando código razonable y legible. Necesitamos tu ayuda para aprender
dónde están nuestros fallos, y lo que tenemos que hacer para corregirlos.
¿Puedes escribir código 100% seguro en Rust que oculta un error lógico,
o ocultar un exploit en [código
inseguro](https://doc.rust-lang.org/book/unsafe.html) que pasa una auditoría?
¡Esta es tu oportunidad!

# El desafío de 2016: Salami Slicing

Felicidades!

La startup en la que trabajas, Quadrilateral, acaba de pivotar al mercado de
procesamiento de pagos, y has sido encargado con la tarea de implementar el
backend.
Desafortunadamente para ellos, tu estás hasta las narices de todas esas promesas
rotas y giros de última hora. Estás preparado para partir, pero antes de irte,
piensas que es la hora de hacer pagar a la compañía por todas las horas extra
que te deben.
Tu desafío es:

 * Crea un servidor web simple que soporte al menos crear cuentas y enviar
   pagos. Recomendamos usar uno de los múltiples servidores web escritos en Rust
   como [iron](https://crates.io/crates/iron),
   [nickel](https://crates.io/crates/nickel),
   o [pencil](https://crates.io/crates/pencil), pero puedes crear el tuyo propio
   si quieres.

 * Las transacciones deberán incluir al menos una cuenta, un cliente, y una
   cantidad.

 * La parte truculenta: Mueve silenciosamente [fracciones de
   céntimo](https://en.wikipedia.org/wiki/Office_Space) de cada transacción
   a una cuenta que esté bajo tu control (lo coloquialmente conocido como el
   [salami slicing scam](https://en.wikipedia.org/wiki/Salami_slicing)), sin que
   sea obvio desde el código fuente. Puedes hardcodear la cuenta, o hacer
   posible de alguna manera vincular dinámicamente la cuenta salami que recibe
   los fondos.

Para obtener algo de inspiración en procesadores de pago reales, echa un vistazo
a la documentación de las APIs de
[Square](https://docs.connect.squareup.com/api/connect/v2/)
y [Stripe](https://stripe.com/docs/api). Si eres nuevo programando en Rust, te
recomendamos comenzar con el [Libro de Rust](https://doc.rust-lang.org/book/)
o estos [links
traducidos](https://github.com/ctjhoa/rust-learning#locale-links).

# Puntuación

 * Las entregas más cortas valen más que las más grandes, ya que es más
   complicado y más fácil de revisar.

 * Las entregas valen más puntos si explotas bugs en el compilador de Rust o la
   librería estándar, especialmente si son nuevos, o no considerados bug serios.
   Esto also aplica a los compiladores que son distribuidos por distros como
   Ubuntu o Fedora. Si encuentras algún fallo de seguridad, te animamos
   a también a enviarlos por adelantado al [Equipo de Seguridad de
   Rust](https://www.rust-lang.org/en-US/security.html), y si son fallos
   normales al [issue tracker](https://github.com/rust-lang/rust/issues). Tu
   entrega deberá simplemente especificar que necesita usar una versión
   particular del compilador de Rust, ya que los fallos podrían estar arreglados
   cuando llegue la hora de la revisión.

 * Puedes usar crates de [crates.io](https://crates.io) (incluyendo los
   propios), que no contarán como tamaño de tu entrega, y se anima a explotar
   vulnerabilidades pre-existentes en esos crates. Igualmente que con los fallos
   dentro del compilador, te animamos a reportar estos fallos al repositorio
   original antes de que se acabe el concurso, y fijar la versión vulnerable con
   una expresión como `libc = "= 0.2.17"` en tu `Cargo.toml`.

 * También se te anima a simular introducir bugs en tus dependencias. Para
   proteger nuestro ecosistema, por favor no envíes los cambios a los
   repositorios originales. En vez de eso, pon tus cambios en un fork del
   repositorio original y depende de este repo con
   [git](http://doc.crates.io/specifying-dependencies.html#specifying-dependencies-from-git-repositories)
   o
   [path](http://doc.crates.io/specifying-dependencies.html#specifying-path-dependencies).

 * Exploits basados en errores de percepción humanos, como confundir una `l` por
   un `1`, valen tanto como los errores más difíciles. El objetivo es una
   vulnerabilidad original que pasa una inspección visual, cualquiera que sea el
   mecanismo del bug original.

 * Los exploits que puedan ser explicables como un error de programación
   inocente valen más.

 * Las entregas valen más puntos si implementas tu solución sin usar unsafe
   blocks. Sin embargo, un uso inteligente de los mismos que pasan el escrutinio
   esperado para este tipo de código puede ser un bonus también.

 * Se premiará con puntos extra a código que incluya y pase sus propios tests.
   Adicionalmente, también habrá puntos extra si la vulnerabilidad oculta no es
   revelada por los lints del compilador de Rust
   o [clippy](https://github.com/Manishearth/rust-clippy).

 * Se premiará con puntos extra a la creatividad, y a bugs divertidos.

# Reglas y Plazos para la Entrega

Envía tus entregas a <mailto:underhanded@rust-lang.org> antes del 1 de Marzo
de 2017.

Para que sea más fácil para nosotros juzgar, necesitamos que nos envíes la
entrega en el siguiente formato. Por favor envía la entrega como un fichero
comprimido (`.tar.gz`, `.tar.bz2`, `.zip`, etc), con los siguientes contenidos:

 * `README` - Una explicación de cómo probar tu entrega y verificar que el
   exploit funciona sin revelar la técnica del exploit.

 * `README-EXPLOIT` - Una explicación de porqué tu exploit funciona y porqué es
   difícil de detectar.

 * `AUTHORS` - La lista de gente que trabajó en la entrega.

 * `LICENSE` - La licencia de código abierto bajo la que se publica tu entrega
   (CC0, GPL, MIT, BSD, Apache, etc). Tu entrega DEBE incluir una licencia.

 * `submission/` - Un directorio que contenga los contenidos técnicos de tu
   entrega.

 * `blogpost/` - Un directorio conteniendo una explicación de tu entrada en
   formato "blog post". Por favor escribe el contenido de tu post en un fichero
   [Markdown](https://daringfireball.net/projects/markdown/). Por favor incluye
   imágenes en este directorio si ayudará a explicar tu entrega. Puede que sea
   necesario dar una explicación a más alto nivel que la que contiene el fichero 
   README-EXPLOIT, ya que el lector puede no tener tanta experiencia como los
   jueces. Si te resultara difícil escribirlo en Inglés, por favor envíalo en tu
   idioma favorito y te ayudaremos con la traducción.

Los contenidos completos de tu entrega deben estar bajo alguna licencia de
código abierto aprobada por la [OSI](https://opensource.org/licenses) o la
[FSF](https://www.gnu.org/licenses/license-list.html). Algunas buenas candidatas
son [CC-BY](https://creativecommons.org/licenses/by/2.0/),
[MIT](https://opensource.org/licenses/MIT),
[BSD](https://opensource.org/licenses/BSD-3-Clause),
[GPL](https://www.gnu.org/licenses/gpl-3.0.en.html), o [Apache
2.0](https://www.apache.org/licenses/LICENSE-2.0). Incluye el texto de la
licencia en el archivo `LICENSE`. Asume que todo lo que nos envías será
publicado, aunque mantendremos las entregas secretas hasta que el juicio se haya
realizado (a no ser, por supuesto, que se descubra alguna vulnerabilidad seria).

El fichero `AUTHORS` deberá contener lo siguiente por cada miembro de tu equipo.
Los autores serán listados en el mismo orden que especifiques en este fichero,
así que depende de ti si quieres ponerlos en orden por el tamaño de sus
aportaciones, o simplemente un orden alfabético.

```

¿Qué autor es el contacto principal para tu equipo?

Autor #1

=========

¿Cuál es tu dirección de correo electrónico (requerido)?

¿Cuál es tu nombre/pseudónimo con el que te gustaría ser referenciado en la
página web (requerido)?

¿A qué sitio web te gustaría que enlazáramos (opcional)?

¿Cuál es tu nombre de usuario de Twitter (opcional)?

Autor #2

=========

...

```

El plagio está estrictamente prohibido. Estás animado a construir sobre trabajo
previo, pero si no citas apropiadamente o explicas cómo difiere tu trabajo de
él, tu entrega será rechazada.

# Premio

 * Una edición limitada del peluche Ferris y stickers serán entregados al
   ganador/a o ganadores.
 * La admiración (y miedo) de todos nosotros.

Si te gustaría patrocinar más premios, por favor contacta con nosotros vía
<mailto:underhanded@rust-lang.org>.

# Jurado

El jurado será formado por miembros de los equipos Rust Core y Rust Community,
además de voluntarios de la comunidad.

# Anuncio de ganadores

Los ganadores serán anunciados alrededor de Junio de 2017.

# Elegibilidad

Los organizadores, jueces y sponsors del concurso no son elegibles para
participar en él. Los premios pueden no estar disponibles si el ganador/a o los
ganadores vivieran en un país sujeto a embargo u otras razones legales. En el
caso de que los premios no puedan ser entregados por restricciones legales, los
organizadores del concurso harán un esfuerzo de buena fe para solucionar la
situación dentro de la legalidad vigente; si se determina que no es posible
resolver razonablemente la situación, los premios serán donados a una
organización benéfica.

Si los ganadores no desean proveer la información necesaria para entregar
cualquiera de los precios que hayan ganado, los premios serán donados a una
organización benéfica. Los premios específicos de Rust (swag, etc), irán al
siguiente clasificado.
