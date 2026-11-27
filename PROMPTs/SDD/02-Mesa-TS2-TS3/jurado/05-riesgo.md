Ya revisé los informes y comprobé los anclas clave en la evidencia y en el repositorio. Este es el veredicto:

# Juez · Riesgo

**Pregunta:** ¿la corrección es reversible? ¿Qué se rompe si sale mal?

## Votos

- **P1 (TS-3) = A.** Es la opción más reversible. Ya está construida y medida: 12 IGUAL y 0 DISTINTO (`prueba-real.txt:72-142`). Si falla, el plan alternativo ya está firmado: B, con Bumble como puente (R:15, `Respuestas-A-Preguntas.md:15`), que S5 mostró viable. Lo que se pierde si A sale mal son las líneas de C# ya escritas, no la épica.
- **P2 (TS-2) = A.** Aceptar el emparejamiento emulado para la 1.0 se puede corregir en la segunda etapa sin rehacer nada, porque el intake ya pone ahí la medición de la 58HB6 real. B frena la 1.0 de una forma difícil de deshacer y no corrige la falla observada, que es del lado emulado (R8).

## Hallazgos

- **h1 · procedente.** El primer vínculo dejó `state=12`, pero el RFCOMM venció (`prueba-real.txt:44-47`). Con el CE-2 actual ese vínculo inservible cuenta como éxito, y así entra en la 1.0 un vínculo que no sirve. Endurecer el criterio es barato y se puede volver atrás.
- **h2 · procedente.** Es la única salida hacia B. Si no se asienta el consumo, el disparador de 2,5 M no puede activarse y la decisión A queda cerrada por omisión. Escribirlo en §4 la mantiene reversible.
- **h3 · procedente.** El riesgo de descartar C por error es bajo: con la misma pila, C es A sin dirección fija. Una salvedad: S6a sale de la prueba corta, que es local y que el ADR excluye como evidencia (ADR:23). §1 tiene que cambiar o hay que publicar la prueba corta.
- **h4 · procedente.** La topología del contenedor aparte no se probó nunca (las corridas usaron `docker exec`). Si falla, se cae la premisa del espacio de red compartido. Atarla a LAZ-0005 y fijar la versión (emulador 37.2.12, API 37) deja un punto concreto para volver a probar cuando se actualice netsim («may still be evolving»).
- **h5 · procedente.** Hay código inalcanzable con prueba en verde: el periférico activa SSP (`PerifericoBluetooth.cs:145`). Eso da una confianza falsa. Conviene **declararlo** sin criterio y no borrarlo: borrarlo cuesta caro si la 58HB6 empareja por PIN.
- **h6 · procedente.** Lo comprobé: `prueba-real.txt:190` es el **primer RFCOMM después del vínculo** (conexión 1, 64 KiB) y su hash no aparece en ningún `SENT`. Es justo el dato que mide h1. Si no se explica, el nuevo CE-2 se apoya en una transferencia sin origen comprobado.
- **h7 · procedente.** Lo comprobé: la punta de la rama es `05789b1`, y `5952ba9` (que cita el contrato) ya no está en el `git log` de la rama, por el rebase. Además, `mutacion.txt` tiene cambios sin commit. Si no se fija el commit, el sustento del ADR no se puede reproducir y una reversión no tiene contra qué compararse.
- **h8 · procedente.** Si alguien vuelve a mandar pings, netsim corta el flujo, y en la primera corrida eso pasó dos veces en unos 7 min (`prueba-real.txt:152,167`). Hoy eso sólo se detecta con una prueba real. Una prueba unitaria barata lo evita. No bloquea la decisión: va como pendiente en §4.

## Qué se rompe si sale mal, y cómo se revierte

- **A cae (por el presupuesto, el contenedor o la versión):** se vuelve a la persona con B. El costo es el código ya hecho. Se puede revertir si h2 y h4 quedan escritos.
- **TS-2 cae (la 58HB6 real difiere):** se corrige en la segunda etapa. El caso a reproducir depende de los permisos, no del emparejamiento (R6; lo leí sólo a través del informe, NO VERIFICADO).
- **Riesgo sin red:** un vínculo trabado en «AUTHENTICATING» no tiene un procedimiento de recuperación escrito (H6). Va en §4.

**NO VERIFICADO:** que las pruebas den 20 de 20 en `05789b1` (no corrí `dotnet`), la norma privada y los logs de `spike/`.

VOTO: P1=A P2=A
