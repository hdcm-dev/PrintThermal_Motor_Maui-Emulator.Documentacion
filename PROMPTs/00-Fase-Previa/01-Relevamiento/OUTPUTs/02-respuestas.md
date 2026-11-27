# Respuestas · Ronda 02 · firma del intake 1.1 y propuestas de publicación

> Transcripción de un agente de las respuestas de la persona, dadas por chat el 2026-11-27. Es una salida: el original es el chat (bloques C1 a C4 de §1).
>
> `ronda: 02` · `fecha: 2026-11-27` · `canal: chat`
> `responde: persona fernandofilipuzzi-utn` · `tipo: persona` · `rol: Product Owner` · `mandato: —`
> `transcribe: agente` · `original: mensajes del chat del 2026-11-27 (bloques C1 a C4 de §1 de este archivo) sha256: 101872423d4ad87e31442793428f7cbea1d398059edf9ff42e33566ef8803067` · `contexto: —`

El sha256 del bloque C1 está en la cabecera. Los de los otros bloques: C2 `076149b3b7ad0aff5743fd874b24c8849c41ad111388883b3d2927a4f0d70c24`, C3 `6e36b217c2f4e34b78603696c1179bf2325dd9242607aed5d429b9a3b1560026`, C4 `66817f8c1e013e57d7c8bfc79e13128853910b600fd2dc2cf1aabdd341168fc9`. Cada huella es la del bloque: sus líneas, con su salto final, sin las líneas `~~~text` y `~~~`.

## 1. Testimonio

**C1** · primera respuesta, sobre las preguntas 2 a 5

~~~text
te pregunto, sobre ` (recomendada): cada release genera una imagen de contenedor con versión fija, y se compila al vuelo sólo para desarrollar el emulador.` como seria? - eso queda publicado en github ? y vos luego te lo descargaria para proseguir con el montarje de la scene 

sobre 3. tenes razon es publico, podes usar los runners de github y no necesitamos usar nuestros runners- eso lo podes ver vos , 

sobre 4. si, porque es para lanzar en pruebas internas , incluso en scene donde tengamos que correr diagnostico sobre reportes de fallos - montamos la scene con la impresora emulador y ahi podemos reproducir casos, tal como el que estamos tratando

sobre 5. A
~~~

**C2** · segunda pregunta de la persona

~~~text
Claro publicar el contenedor tendría que darte un token de dockerhub?
~~~

**C3** · después de que el agente explicara que la pregunta 3 pasaba a «sólo runners de GitHub» y que el texto del intake cambiaba (el rótulo es del agente; el bloque es literal)

~~~text
El aprobado de la pregunta 1 es ok
~~~

**C4** · respuesta a «¿confirmás la A de la pregunta 2?» (el rótulo es del agente; el bloque es literal)

~~~text
Ok. No sabía que se podía publicar el contenedor en github . Tiene algún costo?
~~~

## 2. Respuestas por pregunta

Cada respuesta es la palabra de la persona en C1 a C4. La línea «Decidido» la escribe el agente que transcribe, según lo indicado por la sesión CDD; no es palabra literal de la persona.

### P1

Palabra de la persona: C3 («El aprobado de la pregunta 1 es ok»), dada después de que se le dijera que la pregunta 3 cambiaba el texto del intake.
Decidido: aprobación dada con la pregunta 3 resuelta de otro modo que la recomendada, o sea con un texto que cambia. Qué firma esto lo resuelve el intake (§14) con la norma, no esta transcripción.

### P2

Palabra de la persona: C1 («sobre ` (recomendada): cada release genera una imagen de contenedor con versión fija…» como seria? …»), C4 («Ok. No sabía que se podía publicar el contenedor en github . Tiene algún costo?»). Quedan dos preguntas de la persona sin respuesta registrada: dónde queda publicada la imagen y qué costo tiene (C1, C4); y si hace falta un token de Docker Hub (C2).
Decidido: A, release con imagen de contenedor de versión fija; al vuelo sólo en desarrollo.

### P3

Palabra de la persona: C1 («sobre 3. tenes razon es publico, podes usar los runners de github y no necesitamos usar nuestros runners- eso lo podes ver vos»).
Decidido: C, sólo runners de GitHub; no es la opción recomendada (A).

### P4

Palabra de la persona: C1 («sobre 4. si, porque es para lanzar en pruebas internas …»).
Decidido: A, sin autenticación y publicada sólo en la red del contenedor de pruebas.

### P5

Palabra de la persona: C1 («sobre 5. A»).
Decidido: A, la persona como responsable y la sesión que conduce el emulador como mantenedora mientras dure la primera etapa.
