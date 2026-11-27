# Informe · Lector sin contexto

**Pregunta de rol:** ¿alguien que no participó entiende la decisión y trabaja con ADR-0004 sin preguntar? **No, todavía no.** El ADR es corto y está ordenado, pero para entenderlo hace falta abrir la prueba corta, la evidencia de la parcela, LAZ-0005 y el código. Cada pregunta de abajo es un hallazgo.

## Hallazgos

| # | Ancla | Hallazgo → pregunta que haría el lector |
|---|---|---|
| H1 | E2 | `ADR-0004…md:23` dice que la prueba corta «no están publicados ni juzgados, y este ADR no los usa como evidencia». `DEC.md:7` convoca la mesa «cuando ese resultado esté publicado, antes de la primera parcela de la épica». El contrato (§2) la rotula «local, no publicada», y `parcela.md:5` dice `estado: cerrada`. → ¿Se cumplió DEC-001? ¿Quién juzgó S0-S8? El ADR no explica por qué el orden se invirtió; sólo lo explica el contrato §1. |
| H2 | E2 | La opción C figura como «no evaluado» (`ADR-0004…md:29`). Pero S6a la midió: por HCI TCP «dirección … pasó a …; la conexión al vínculo anterior da `read failed`» (`Prueba-Corta.md:23`; `Medios-Y-Factibilidad.md:65`). → ¿C sigue abierta? Con el ADR solo, parece que sí. |
| H3 | E4 | La opción B choca con «Bumble sólo en la prueba corta» (`intake.md:32`). Según `intake.md:93`, un cambio de tecnología vuelve a la persona. → ¿La mesa puede elegir B o sólo recomendarla? El ADR dice «contra … intake §6» pero no dice qué pasa si se elige. |
| H4 | E2 | `ADR-0004…md:20` da por hecho que funciona «compartiendo el espacio de red». En la prueba real el periférico corrió dentro del contenedor del emulador (`prueba-real.txt:18-19`), y LAZ-0005 lo deja «no medido» (`LAZ-0005…md:28`). → ¿Dónde corre el periférico en la 1.0? El ADR no menciona LAZ-0005. |
| H5 | E2 | El título dice «con dirección fija», pero `OpcionesPeriferico.cs:5-24` no tiene dirección: la recibe `TransporteNetsim.Conectar(servidor, direccion, nombre)` (`TransporteNetsim.cs:49`) y el host llega recién en PAR-PTE-04 (D6). Además netsim la invierte (`Prueba-Corta.md:29`). → ¿Qué dirección usa el producto? ¿Quién la fija? ¿En qué orden se escribe? |
| H6 | E2 | En el primer intento, tocar «Pair» a los 31 s dejó a Android en «AUTHENTICATING», y se resolvió cambiando de dirección (`prueba-real.txt:44-47`). → ¿Cómo se recupera un vínculo trabado: otra dirección, olvidar el equipo, borrar el archivo de claves? |
| H7 | C | El emparejamiento pide un toque humano en el diálogo de consentimiento (`prueba-real.txt:52`). El intake pide una «interfaz para pruebas automáticas» (`intake.md:24`). → ¿Quién confirma el diálogo en una prueba de extremo a extremo? |
| H8 | E2 | El PIN «0000» está programado (`OpcionesPeriferico.cs:17`) y lo prueba `ElPinHeredadoSeContestaConElDeLaImpresora` contra un controlador falso, pero RootCanal «se recibe y se ignora» (`Medios-Y-Factibilidad.md:58`). → ¿Ese camino cuenta como requisito o es código que no se puede verificar de punta a punta? |
| H9 | E2 | El ADR no dice con qué versión se midió (emulador 37.2.12, API 37; `prueba-real.txt:7`). Tampoco registra la restricción «sin pings de HTTP/2» (`TransporteNetsim.cs:26`; `prueba-real.txt:146-148`), aunque la fuente advierte que netsim «may still be evolving» (`ADR-0004…md:22`). → Si actualizo el emulador, ¿qué miro primero? |
| H10 | E1 | `grep -rn "tokens\|2,5 millones" cdd/` da una sola línea, `ADR-0004…md:21`. → No hay medición del consumo, así que nadie puede saber si se cruzó el umbral para volver a la persona. |
| H11 | E1 | El contrato (§3) muestra `5952ba9` como punta de la rama. Hoy `git log --oneline -1` da `9054249 PAR-PTE-03: cierre (borrador)…`. Y `parcela.md:85` ya dice «D1 (K2) la decidió una mesa de otro contexto» mientras esta mesa sigue sesionando. → ¿Qué commit se está juzgando? ¿D1 está decidida o no? |
| H12 | E1 | En rojo hubo 13 pruebas nuevas (`rojo.txt:2`, `Failed: 13`); en verde hay 16 (`pruebas.txt:1`). El cierre explica sólo una de las agregadas (`parcela.md:84`). Las otras dos, `HciNetsimTests.*` (el transporte gRPC, D2), no aparecen en rojo. → ¿Faltó el rojo de esas dos? |
| H13 | E2 / C | ADR-0004 tiene `rutas: []` (`ADR-0004…md:6`): el lector no sabe qué código gobierna. Las trazas están sólo en las REQ-HIS. Si un ADR con `gobierno: humano` puede declarar rutas: NO VERIFICADO (la norma es privada). |
| H14 | E2 | Hay términos sin definir en el ADR: RootCanal, SSP / «Just Works» / «variante 3», PA-4, y las citas X:n y R:n (se decodifican recién en `intake.md:40-46`). La 58HB6 sólo se explica en `intake.md:24`. |

## P1 (TS-3) desde mi rol

**A.** Es la única opción que el lector entiende sin pasar por otra decisión:
- es la dirección del intake firmado (`intake.md:50`);
- está construida y medida: descubrimiento 3 de 3, SHA-256 igual 10 de 10, reconexión tras 2 reinicios (`prueba-real.txt` §2-§5);
- B obliga a volver a la persona (H3);
- C está refutada por S6a (H2).

Condición: el ADR tiene que decir *por qué* se descartan B y C con esas citas. Hoy no lo dice.

## P2 (TS-2) desde mi rol

**A (aceptarlo y medir la fidelidad en la segunda etapa).** B contradice lo firmado: la medición de la 58HB6 real va «en la segunda» etapa (`intake.md:35`; PA-3 `intake.md:76`), así que B sería un retorno a la persona y no una opción de la mesa.

Para que un tercero trabaje con A, el ADR tiene que nombrar:
- qué se acepta: SSP con consentimiento sobre netsim, API 37, emulador 37.2.12;
- qué no: el PIN heredado (H8) y el comportamiento de la 58HB6 real;
- dónde se mide: segunda etapa;
- el riesgo operativo del diálogo y del vínculo trabado (H6, H7).

## P3 · Texto propuesto (ADR-0004 §3 y §4)

> **§3 Decisión.** A: transporte Bluetooth Classic propio en C# sobre el gRPC de netsim (`PacketStreamer/StreamPackets`), con dirección fija que fija el host del servicio. netsim invierte el orden de los bytes de la dirección (prueba corta S6b). Se descarta C porque por HCI TCP la dirección cambia en cada reconexión y rompe el vínculo (S6a). Se descarta B porque contradice «Bumble sólo en la prueba corta» (intake §6); elegirla vuelve a la persona (intake §12). TS-2: se acepta para la 1.0 el emparejamiento SSP con consentimiento medido sobre netsim (Android 17, API 37, emulador 37.2.12; PAR-PTE-03, `evidencia/2026-11-27-prueba-real.txt`). El PIN heredado no es verificable en RootCanal, y el emparejamiento de la 58HB6 real se mide en la segunda etapa (intake §6, PA-3). Orden: la parcela se construyó antes que la mesa por decisión de quien convocó (D1, K2); la prueba corta se leyó como registro local, no publicado.
>
> **§4 Consecuencias.**
> - Código: `src/PrintThermal.Emulator.Bluetooth/`.
> - Sin pings de HTTP/2 hacia netsim.
> - Protobuf escrito a mano (D2): al cambiar la versión del emulador se repite la prueba real.
> - Dónde corre el periférico: abierto en LAZ-0005, se mide en PAR-PTE-05.
> - El diálogo de consentimiento necesita un toque a tiempo. Un vínculo trabado en «AUTHENTICATING» se recupera olvidando el equipo en Android o cambiando la dirección. La confirmación automática en pruebas de extremo a extremo queda pendiente.
> - Riesgos del intake §10 sin cambio: fidelidad sin calibrar y emparejamiento emulado distinto del real.
> - Consumo frente al umbral de 2,5 M de tokens: sin medir.

## Lo que revisé y está bien

- **ADR-0004:** tiene índice y cuatro secciones. Su condición de reemplazo («falla en S2, S3 o S5», `ADR-0004…md:33`) se puede verificar y no se disparó: S2 OK 3/3, S3 OK, S5 OK 5/5 + 5/5 (`Prueba-Corta.md:19-22`).
- **El ADR no se tocó:** `git diff 5952ba9 9054249 -- cdd/corpus/decisiones/` sale vacío, como corresponde a `gobierno: humano`.
- **Cifras del contrato:** `grep -cE "^\s+Passed "` sobre `pruebas.txt` da 20, tanto en HEAD como en la copia de trabajo. Los 10 envíos IGUAL del contrato coinciden con `prueba-real.txt:72-121`.
- **Mutación:** seis mutaciones sobre REQ-01 a REQ-03, las seis en rojo (`mutacion.txt`).
- **Datos en la evidencia:** la dirección de Android está enmascarada y la URL de netsim aparece como `<loopback>:<puerto gRPC>`.
- **LAZ-0005:** registra el desvío de la red con parcela destino (PAR-PTE-05) y un criterio medible.

**NO VERIFICADO:**
- `Rules-Decisiones.md` y `Knowledge-Mesa` §5 (norma privada).
- El extracto X:10.
- La página pública de Bumble (no la abrí).
- Los registros en `spike/`.
- Si `Prueba-Corta.md` está versionado: el comando de git sobre el repositorio de documentación no se aprobó.
