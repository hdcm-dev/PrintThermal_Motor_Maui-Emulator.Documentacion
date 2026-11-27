# Juez · Coherencia

**Pregunta:** ¿reabre una decisión cerrada? ¿Es coherente con lo firmado y con los veredictos previos?

## 1) Votos

- **P1 (TS-3) = A.** Es la dirección firmada: «Pila propia en C# después de la prueba corta» (`intake.md:50`). También cumple la regla fijada de antemano en Medios («S2-S5 bien y S8 bien = seguir con (a)»), y la condición de reemplazo de ADR:33 no se disparó.
  - B no la puede elegir la mesa: «Bumble sólo en la prueba corta» (`intake.md:32`). Pero es el plan alternativo firmado en R:15 («si supera 2,5 millones de tokens, se vuelve a la persona con la alternativa de dejar Bumble como puente»; abierto y confirmado). Elegirla hoy reabriría esa restricción firmada; dejarla como disparador no reabre nada.
- **P2 (TS-2) = A.** PA-3 y TS-4 ya están respondidas por el PO: la medición de la 58HB6 real va en la segunda etapa (`intake.md:35,76-77`). B reabriría esas dos respuestas firmadas.

## 2) Hallazgos

- **(h1) Procedente.** Endurece CE-2 sin relajarlo, así que no contradice lo firmado. Condición: va como medición en el ADR o en el REQ. Cambiar el texto de CE-2 en el intake (§9, firmado) sería un retorno según §12.
- **(h2) Procedente.** No reabre nada: ejecuta una decisión firmada que hoy no figura en ningún §3 o §4. El disparador está en R:15, `intake.md:50` y ADR:21. Sin consumo asentado, nadie puede saber si se cumple.
- **(h3) Procedente.** C no estaba cerrada (ADR:29 dice «no evaluado»), así que descartarla no reabre nada. Para que sea coherente hay que publicar la prueba corta o corregir ADR:23, que hoy la excluye como evidencia. DEC-001 además pide que el resultado esté «publicado».
- **(h4) Procedente.** El intake firma «contenedor aparte unido a la red del contenedor del emulador» (`intake.md:50`). Si el ADR dice que vale sólo para el periférico dentro del contenedor del emulador y no lo ata a LAZ-0005 (que existe en `cdd/lazo/`), relaja en silencio un requisito firmado. Declarar para qué versión vale va en la misma línea.
- **(h5) Procedente.** Es coherente con PA-3 y TS-4: no promete un criterio que el medio emulado no puede dar. Retirar ese camino del código es una decisión K1 de la parcela, no de la mesa.
- **(h6) Procedente.** Lo comprobé: `prueba-real.txt:190` registra `CIERRE conexion=1 bytes=65536` con un hash que no está en ningún `tx: … SENT`. La evidencia que sostiene a A tiene que ser coherente consigo misma.
- **(h7) Procedente.** Hoy la punta de la rama es `05789b1`, después de un rebase (`git log`), y `mutacion.txt` tiene cambios sin commit. El contrato cita `5952ba9` y los informes citan `9054249`. Sin un commit fijado, el veredicto no se puede contrastar con nada.
- **(h8) No procedente desde mi pregunta.** No reabre ni contradice ninguna decisión. Es un pendiente técnico válido de la parcela (K1), no una condición de TS-2 ni de TS-3.

## Coherencia de procedimiento (no cambia el voto)

- DEC-001 pide la mesa «antes de la primera parcela» y con la prueba corta publicada. Las dos condiciones se invirtieron por D1 de quien convocó. Corresponde asentarlo como desvío en DEC.md o en el ADR.
- El cierre de `parcela.md` ya afirma que «D1 la decidió una mesa» mientras la mesa sesiona. Hay que corregirlo cuando salga el dictamen.
- NO VERIFICADO: la norma privada (`Rules-Decisiones`, `Knowledge-Mesa`) y que la evidencia sea la misma antes y después del rebase.

VOTO: P1=A P2=A
