# Juez · Impacto

Pregunta: si no se corrige, ¿qué pasa concretamente?

## Votos
- **P1 = A.** Está construida y medida: 12 envíos con el mismo SHA-256 en los dos extremos (IGUAL), 0 distintos, y 2 reinicios sin reemparejar (`prueba-real.txt:72-142`). Si no se elige A, se pierde la única opción con evidencia de la parcela. B solo se abre por el disparador firmado de R:15, y C no aporta nada que A no tenga.
- **P2 = A.** Con B la épica queda frenada por una medición que el intake pone en la segunda etapa (`intake.md:35`). Además, medir la impresora real no arregla el vínculo trabado que se observó (R8).

## Hallazgos
- **h1 · procedente.** Si no se corrige, CE-2 aprueba un vínculo que no se puede usar. Pasó en el primer intento: `state=12`, la seguridad quedó en «AUTHENTICATING» y el RFCOMM venció por tiempo (`prueba-real.txt:44-47`, comprobado). Solo 1 de 2 emparejamientos terminó usable, y la 1.0 saldría sin un criterio que lo detecte.
- **h2 · procedente.** Si no se corrige, se puede cruzar el umbral firmado sin que nadie lo vea. R:15 dice textualmente «se vuelve a la persona con la alternativa de dejar Bumble como puente» (`Respuestas-A-Preguntas.md:15`, comprobado). La estimación llega a 2,5 M (`Medios…md:94`), faltan dos parcelas de pila y no hay consumo asentado.
- **h3 · procedente.** Si no se corrige, el ADR sigue diciendo «no evaluado» (ADR:29) y un lector lo toma como una opción abierta que hay que reevaluar (H2 del Lector). Salvedad: S6a sale de una prueba corta que no está publicada. O se publica, o el ADR la cita como registro local.
- **h4 · procedente.** Si no se corrige, la 1.0 da por supuesta una topología (contenedor aparte) que nunca se midió. Y si cambia la versión del emulador, el ADR no dice qué volver a correr. netsim es un protocolo interno, escrito a mano y que «may still be evolving».
- **h5 · procedente.** Si no se corrige, una prueba unitaria en verde da por cubierto un camino que contra Android no corre. SSP está activo (`PerifericoBluetooth.cs:145`, comprobado), y alguien leería que el PIN 0000 de la 58HB6 está soportado. Que la norma Core imponga SSP cuando los dos lados lo soportan: NO VERIFICADO.
- **h6 · procedente (impacto bajo).** La línea 190 es `conexion=1` con 65536 bytes, cuatro segundos después del primer RFCOMM abierto, y no tiene `SENT` (comprobado). Si no se explica, «0 DISTINTO» no se puede auditar para esa transferencia. Si resulta ser el primer envío tras el vínculo, es justo la evidencia que pide h1.
- **h7 · procedente (el más grave en procedimiento).** La punta de la rama es `05789b1` (comprobado con `git log`). Los commits `5952ba9` y `9054249` que citan el contrato y tres informes ya no están en la rama. Además, `mutacion.txt` tiene cambios sin commit (estado de git). Si no se corrige, el ADR queda apoyado en una evidencia que nadie puede reproducir desde el repositorio.
- **h8 · procedente (impacto bajo, va a una parcela y no al ADR).** El arreglo es solo un comentario y la ausencia de pings (`TransporteNetsim.cs:26`). Ninguna prueba la exige: comprobé que `HciNetsimTests.cs` no mira los pings. Si alguien los vuelve a poner, netsim corta el flujo cada pocos minutos (`prueba-real.txt:152,167`). El servicio reintenta en 2 s, pero corta tickets a mitad de envío, y solo se vería en una prueba real.

**NO VERIFICADO:** la norma privada (`Rules-Decisiones`, `Knowledge-Mesa`), los registros de `spike/`, el binario `c437…`, y que la evidencia sea la misma antes y después del rebase.

VOTO: P1=A P2=A
