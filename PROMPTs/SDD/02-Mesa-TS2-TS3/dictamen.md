# Mesa TS-2 y TS-3 · Dictamen

## Índice

1. [Composición](#1-composición)
2. [Veredicto](#2-veredicto)
3. [Hallazgos](#3-hallazgos)
4. [Texto propuesto para ADR-0004](#4-texto-propuesto-para-adr-0004)
5. [Plan y cierre](#5-plan-y-cierre)

## 1. Composición

- Contrato: `contrato.md`. Fecha: 2026-11-27.
- Comisiones a ciegas, cada una en otro contexto: Requisitos (`informes/01-requisitos.md`), Verificación (`informes/02-verificacion.md`) y Lector sin contexto (`informes/03-lector.md`).
- Refutador, último y después de leer a las comisiones: `informes/04-refutador.md`.
- Jurado de cinco contextos distintos: Evidencia, Impacto, Costo/beneficio, Coherencia y Riesgo (`jurado/`).
- Todos con el mismo modelo (`claude -p`, claude-opus-5-5), por eso la garantía es reducida y se declara así.
- Quien convocó y consolida es el contexto que ejecutó PAR-PTE-03: no vota y no reescribe los informes, que están verbatim.
- Variables descartadas, con su motivo en el contrato §5: arquitectura y seguridad.
- Commit juzgado, rama `parcela/PAR-PTE-03`: `ade3907` para el código y la evidencia. Los informes leyeron puntas anteriores (`5952ba9`, `9054249`, `05789b1`). Entre ellas cambian el rebase sobre `main` y lo que corrigieron estos mismos hallazgos, nunca el camino que midió la prueba real (`evidencia/2026-11-27-prueba-real.txt`, «Código medido»).

## 2. Veredicto

| Pregunta | Voto del jurado | Decisión |
|---|---|---|
| P1 (TS-3) | A 5 de 5 | **A.** Transporte propio en C# sobre el gRPC de netsim, con dirección fija |
| P2 (TS-2) | A 5 de 5 | **A.** Para la 1.0 se acepta el emparejamiento SSP con consentimiento sobre netsim; la fidelidad frente a la 58HB6 real se mide en la segunda etapa |

## 3. Hallazgos

| ID | Hallazgo | Jurado | Qué se hizo |
|---|---|---|---|
| h1 | CE-2 se mide como «vinculada y primer RFCOMM íntegro sin reemparejar» | procedente 5/5 | La medida de CE-2 la firmó la persona (visión): va a la Review con LAZ-0011. La evidencia de PAR-PTE-03 ya cumple la medida endurecida con la segunda dirección |
| h2 | El disparador firmado de R:15 (más de 2,5 M tokens vuelve a la persona con B) va en §4 y el consumo se asienta | procedente 5/5 | En el texto propuesto (§4 de este dictamen); el consumo de PAR-PTE-03 queda NO VERIFICADO en su cierre |
| h3 | C se descarta por S6a | procedente 5/5 | En el texto propuesto |
| h4 | El contenedor aparte queda atado a LAZ-0005 y el ADR declara para qué versión vale | procedente 5/5 | En el texto propuesto |
| h5 | El camino del PIN heredado no se recorre con SSP activo y se declara sin criterio | procedente 5/5 | En el texto propuesto y en el cierre de la parcela |
| h6 | La transferencia sin SENT de la evidencia se explica | procedente 5/5 | Aplicado: es el envío previo a la serie, también igual |
| h7 | El dictamen fija el commit juzgado | procedente 5/5 | Aplicado (§1) |
| h8 | Falta una prueba que impida volver a mandar pings de HTTP/2 | procedente 4/5 | Aplicado: `ElTransporteNoMandaPingsDeHttp2` y mutación M11 en rojo |

## 4. Texto propuesto para ADR-0004

Para el lote de K2 de la Review de SPR-01. ADR-0004 tiene `gobierno: humano`: lo cambia la persona, no la mesa.

> **§3 Decisión.** A: transporte Bluetooth Classic propio en C# sobre el gRPC de netsim (`PacketStreamer/StreamPackets`), con dirección fija en `ChipInfo.chip.address` (netsim la toma en orden invertido, prueba corta S6b).
>
> - B (puente con Bumble) no la elige la mesa: es la alternativa firmada (R:15). Se activa si la pila supera 2,5 M tokens, y entonces vuelve a la persona.
> - C (HCI por el puerto TCP de netsim) está dominada: con la misma pila, la dirección no queda fija y el vínculo se rompe (S6a).
> - TS-2: para la 1.0 se acepta el emparejamiento SSP con consentimiento sobre netsim (clave sin autenticar, tipo 4). El caso a reproducir depende de los permisos de Android, no del emparejamiento. La fidelidad frente a la 58HB6 real (método SSP o PIN heredado, diálogo, tipo de clave, registro SDP) se mide en la segunda etapa (intake §6, PA-3, TS-4).
> - Sustento: PAR-PTE-03 (`ade3907`), con descubrimiento 3 de 3, SHA-256 igual 10 de 10 y reconexión sin reemparejar 2 de 2, y la prueba corta.
> - Vale para: emulator 37.2.12 y Android 17 / API 37, con el periférico dentro del contenedor del emulador. El contenedor aparte se rige por LAZ-0005.
>
> **§4 Consecuencias.**
>
> - Vuelve a la persona, con B como alternativa, si se cumple cualquiera de estas condiciones:
>   - el consumo asentado de la pila supera 2,5 M tokens; las parcelas de la pila asientan su consumo;
>   - falla la prueba real sobre la versión declarada;
>   - el contenedor aparte no funciona (LAZ-0005).
> - El camino del PIN heredado no se recorre con SSP activo en los dos lados, y RootCanal no valida el PIN: no tiene criterio en el medio emulado.
> - D2 (protobuf escrito a mano) es revisable hacia los paquetes de gRPC que autoriza R:15. Al cambiar la versión del emulador se repite la prueba real. No se mandan pings de HTTP/2 a netsim.
> - Un vínculo quedó inservible tras el primer emparejamiento; la causa no está separada (consentimiento tardío o binario con pings, LAZ-0011).
> - Siguen sin verificar la librería cliente y las capas del fabricante. Los riesgos del intake §10 no cambian.

## 5. Plan y cierre

- La aplicación del texto de §4 sobre ADR-0004 la decide la persona en la Review. Nadie más lo aplica.
- Aplicado en la rama de PAR-PTE-03: h6, h7 y h8.
- Deuda declarada:
  - el consumo de tokens no se asentó (h2, LAZ-0012);
  - el contenedor aparte (LAZ-0005);
  - la entrega al almacén (LAZ-0010, del auditor de cierre);
  - el vínculo trabado (LAZ-0011).
- Capas a revalidar si la persona cambia la medida de CE-2: la visión y REQ-EPI-Medio-Emulado.
- Parada: con un ciclo (`ciclos_max: 1`), sin hallazgos procedentes abiertos fuera de la deuda declarada.
