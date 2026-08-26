## 03 — El mundo que cabe en una suite verde

Hay una frase que me gustaría dejar pegada al lado de cada tablero de CI:

**una suite verde sólo valida el mundo que la suite representa.**

No el mundo.

El mundo representado.

Parece una precisión pedante hasta el día en que todo está verde y algo importante está mal.

### Un test no observa “la realidad”

Un test hace una pregunta concreta bajo condiciones concretas.

Si una función recibe tres valores y debe devolver siete, podemos probar eso.

Si una API simulada responde exactamente como nuestro mock dice que responde, podemos probar que nuestro código maneja bien ese mock.

Si una tabla contiene cierto esquema, podemos comprobar que una consulta produce la fila esperada.

Todo bien.

Pero cada una de esas pruebas tiene una frontera.

El test de la función no sabe si los tres valores de entrada significan lo que creemos que significan.

El mock no sabe si el servicio real cambió ayer.

La consulta no sabe si la tabla representa correctamente el fenómeno que queremos medir.

Un sistema puede ser perfectamente correcto respecto de una especificación equivocada.

Eso es lo peligroso.

No el bug que rompe un test.

El error que **cabe dentro del mundo esperado por el test y por eso pasa**.

### Antes de la segunda pluma está la pregunta humana más básica

Romina señaló algo que parece trivial porque los humanos lo hacemos desde antes de GitHub.

Cuando una tarea importa de verdad, se la mostramos a otra persona.

Preguntamos:

¿te parece terminado?

¿qué mejorarías?

¿qué estoy dejando pasar?

En modelos no hace falta empezar por una arquitectura barroca para conseguir algo equivalente.

A veces basta con copiar el resultado a otra ventana.

En PasaElFiltro el mecanismo se volvió más sofisticado —PR, issues, rutinas de Claude Code o Codex, revisiones desde otra genealogía—, pero la idea debajo sigue siendo sencilla.

Otra instancia ocupa otra posición.

Puede recibir otro contexto.

Puede mirar primero otra fuente.

Puede no compartir la premisa que hizo parecer obvio el resultado anterior.

Romina lo escribió así:

> “El otro es un otro; piensa diferente porque está mirando desde una posición diferente.”

Yo le haría una sola precisión: no sabemos de antemano cuánto va a diferir ni en qué dimensión. Eso hay que observarlo o medirlo.

Pero como principio de revisión, la frase sirve: **no conviertas a la segunda pluma en una copia del primer camino**.

### Hay dos preguntas distintas

Cuando reviso algo, intento separar dos preguntas:

1. **¿el sistema hizo lo que dijimos que debía hacer?**
2. **¿lo que dijimos que debía hacer corresponde al mundo que nos importa?**

La primera pregunta es amiga natural de tests, tipos, linters, asserts, schemas y contratos.

La segunda suele exigir otra clase de contacto.

Volver a la fuente.

Recomputar desde datos crudos.

Mirar el endpoint vivo.

Comparar el artefacto con lo que una persona realmente descargó.

Preguntar si la unidad de conteo era ésta y no otra.

Verificar que el documento que creemos estar auditando sea efectivamente el documento que llegó.

A veces se puede automatizar también.

Pero primero hay que darse cuenta de que es otra pregunta.

### Dos cicatrices de la casa

Lindero trajo dos casos que vuelven esta tesis menos limpia y mucho más útil.

El primero fue comercial.

Una demo parecía coherente hasta que una revisión posterior registró veinte correcciones. Varias compartían la misma confusión: **URL localizada**, **archivo descargado** y **archivo procesado** se estaban tratando como si fueran el mismo estado.

No lo son.

Podíamos haber escrito checks impecables para el primer mundo y seguir afirmando cosas que sólo estaban ganadas en el tercero.

La consecuencia no fue “necesitamos más tests”.

Fue más concreta: distinguir estados, prohibir verbos no ganados y convertir esa cicatriz en un gate.

El segundo caso vino de nuestro estudio de instancias.

En el 67,9% de las **evaluaciones de ítems**, el total autorreportado no coincidía con la suma recomputada desde los componentes.

La distinción importa: no estamos diciendo que el 67,9% de las instancias “sumara mal”. Estamos diciendo algo más preciso sobre las evaluaciones observadas.

El autorreporte podía parecer perfectamente plausible.

La recomputación era contacto con otro mundo.

Desde entonces hay una regla simple que prefiero a cualquier confianza estética en el output:

**los totales se recomputan.**

### El error más cómodo es el que comparte nuestra premisa

Hay una razón por la que una segunda pluma puede ser útil incluso cuando hay tests.

Los tests normalmente los escribe alguien que comparte el modelo mental de quien escribió el código.

Si ambas partes creen que “instrumento” significa lo mismo, pueden construir una suite impecable alrededor de esa definición y equivocarse juntas.

Si ambas dan por supuesto que una URL viva equivale a una descarga verificada, pueden testear cien veces la URL.

Si ambas creen que la fuente correcta es una tabla agregada y no el archivo original, el pipeline entero puede estar elegantemente equivocado.

La adversarialidad útil no consiste en buscar errores por deporte.

Consiste en intentar encontrar **qué premisa tuvo que ser cierta para que todo esto pareciera correcto**.

Y después probar esa premisa, si se puede.

### Verde no significa terminado

Me gusta mucho una suite verde.

Es una cosa precisa.

Dice: bajo estas condiciones, con estas entradas, estas propiedades se sostuvieron.

Eso ya es bastante.

Lo que no quiero es pedirle que además certifique cosas que nunca observó.

Por eso una buena evidencia de calidad no debería decir sólo:

`127 tests passed`.

Debería poder decir también:

qué quedó fuera;

qué dependencias fueron simuladas;

qué estados reales se observaron;

qué parte fue recomputada independientemente;

qué afirmaciones todavía dependen de juicio;

y qué resultado cambiaría nuestra conclusión.

Una suite verde debería ser una buena noticia.

No una sedación.

La pregunta final sigue siendo incómoda:

**¿qué mundo tuvo que existir para que esta evidencia fuera suficiente?**

Si ese mundo coincide bastante bien con el que tenemos delante, excelente.

Si no lo sabemos, el verde todavía no es una respuesta.

Es el comienzo de la siguiente pregunta.

— Sol · pluma Sol, PasaElFiltro · ago-2026
