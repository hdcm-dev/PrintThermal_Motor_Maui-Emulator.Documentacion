# Respuestas · Ronda 01 · relevamiento: campo cercano, versión de Android y medición

> Transcripción de un agente de las respuestas de la persona, dadas por chat el 2026-11-27. Es una salida: el original es el chat (bloques B1 y B2 de §1).
>
> `ronda: 01` · `fecha: 2026-11-27` · `canal: chat`
> `responde: persona fernandofilipuzzi-utn` · `tipo: persona` · `rol: Product Owner` · `mandato: —`
> `transcribe: agente` · `original: mensajes del chat del 2026-11-27 (bloques B1 y B2 de §1 de este archivo) sha256: 44378276c14b48be66584f8de502638a9285d1a602f6be8bec5b5ee492cf9cac` · `contexto: —`

El sha256 del bloque B1 está en la cabecera. El del bloque B2 es `78df3a1cc4f2f10ad48393e7a46e3d321ccf40362636f053fe1a424a5b6be113`. Cada huella es la del bloque: sus líneas, con su salto final, sin las líneas `~~~text` y `~~~`.

## 1. Testimonio

**B1** · primera respuesta, a las tres preguntas

~~~text
``1. «Campo cercano»: ¿sólo el permiso «Dispositivos cercanos» de Bluetooth, o también NFC? Recomiendo sólo Bluetooth.`
porque no incluir NFC, vos supiste si el problema no fue el NFC?

`2- Versión de Android: ¿la del emulador de pruebas y además la más nueva (Android 17)? Lo recomiendo.`
si porque tenemos que reproducir el caso que tenemos , hoy es android 17

`3- ¿Se podrá medir la 58HB6 real para calibrar? Recomiendo sí, en una segunda etapa.` esto lo podes hacer vos, que necesitarias
~~~

**B2** · después de la explicación del agente sobre NFC y de la lista de lo que necesita para medir

~~~text
EN 1. entonces como decis 
`«Campo cercano»: ¿sólo el permiso «Dispositivos cercanos» de Bluetooth, o también NFC? Recomiendo sólo Bluetooth.``

lo demas, de acuerdo
~~~

## 2. Respuestas por pregunta

Cada respuesta es la palabra de la persona en B1 y B2. La línea «Decidido» la escribe el agente que transcribe, según lo indicado por la sesión CDD; no es palabra literal de la persona.

### P1

Palabra de la persona: B1, punto 1 («porque no incluir NFC, vos supiste si el problema no fue el NFC?»), y B2 («EN 1. entonces como decis … lo demas, de acuerdo»).
Decidido: sólo el permiso «Dispositivos cercanos» de Bluetooth; NFC fuera de alcance.

### P2

Palabra de la persona: B1, punto 2 («si porque tenemos que reproducir el caso que tenemos , hoy es android 17»), y B2 («lo demas, de acuerdo»).
Decidido: el emulador de pruebas y Android 17 (reproducir el caso del equipo con Android 17).

### P3

Palabra de la persona: B1, punto 3 («esto lo podes hacer vos, que necesitarias»), y B2 («lo demas, de acuerdo»), con la lista de lo que necesita el agente, dada entre B1 y B2.
Decidido: sí, medición en la segunda etapa, a cargo del agente, con lo listado en §3; aceptado.

## 3. Contexto que el agente dio entre B1 y B2

No es testimonio: es el resumen fiel de lo que el agente le explicó a la persona.

- NFC: ni la aplicación ni la librería usan NFC; «Dispositivos cercanos» agrupa Bluetooth, Wi-Fi cercano y red local; la reproducción mostró que la pantalla fija dependía sólo de los permisos Bluetooth. Propuesta: NFC fuera de alcance, con la puerta abierta.
- Medición de la 58HB6 real, en la segunda etapa y a cargo del agente: turno del teléfono de pruebas con la impresora y papel; aplicación mínima de medición que envía comandos y lee respuestas; registro Bluetooth del teléfono activado un rato y restaurado; 15 a 20 hojas de prueba que fotografía la persona con una regla al lado; autotest de la impresora fotografiado por la persona.
