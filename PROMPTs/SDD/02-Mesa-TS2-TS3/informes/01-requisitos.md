# Informe · Requisitos

Alcance: ADR-0004, intake 1.2, prueba corta, Medios §2-§3, PAR-PTE-03 (parcela, plan, evidencia) y el código de `Seguridad/`. No leí `informes/`. **Aviso:** la rama avanzó mientras revisaba. El contrato cita `5952ba9`, pero la punta es ahora `9054249` («cierre (borrador)», E1: `git log --oneline -1`). El «20» de pruebas en verde sale de `9054249`; en `5952ba9` la evidencia decía «19 de 19» (E1: `git diff` antes del commit). La mesa tiene que fijar el commit que juzga.

## P1 (TS-3) · Recomiendo A, con el texto corregido
- Está construida y medida: 2406 líneas C# (E1: `wc -l` sobre `src/…Bluetooth/**/*.cs`); descubrimiento 3 de 3; 1 emparejamiento SSP; SHA-256 igual 10 de 10; 2 reinicios sin reemparejar (E2 `prueba-real.txt:21-142`). Hay 0 líneas `DISTINTO` (E1).
- **B no es una opción abierta para esta mesa.** «Bumble sólo en la prueba corta» es una restricción firmada (E2 `intake.md:32`). Elegir B cambia la tecnología (L4) y eso vuelve a la persona (E4 `intake.md:93`). El ADR §2 B la presenta como una opción más débil, «contra Producto en .NET 10», y la funda en «más rápido», que sale de una estimación «NO VERIFICADA» (E2 `Medios…md:90`).
- **C sí se evaluó, y el ADR dice que no.** ADR:29 dice «no evaluado». S6a dio «FALLA»: por HCI TCP la dirección cambia en cada reconexión y el vínculo se rompe (E2 `Prueba-Corta.md:23`; `Medios…md:65`). C queda descartada por el requisito de dirección fija.

## P2 (TS-2) · Recomiendo A, con condiciones verificables
- Recomiendo A (aceptar el emparejamiento emulado para la 1.0) con tres condiciones: CE-2 reforzado, las diferencias con la impresora real enumeradas, y su medición en la segunda etapa. La B (no cerrar la épica hasta medir la impresora real) contradice lo que la persona ya firmó: la medición de la 58HB6 real va en la segunda etapa (E2 `intake.md:35,76-77`).

## Hallazgos
1. **E3 · CE-2 se cumple con un fallo.** CE-2 pide «la impresora figura vinculada en Android» (`intake.md:57`). El primer intento terminó en `state=12`, pero la seguridad quedó en «AUTHENTICATING» y el RFCOMM venció por tiempo (`prueba-real.txt:44-47`). Hay vínculo y no hay uso. El criterio tiene que agregar «y una conexión RFCOMM posterior abre sin reemparejar».
2. **E2 · Un solo emparejamiento exitoso.** El éxito es n=1, con la dirección XX:XX:XX:XX:00:02 (`prueba-real.txt:48-60`). La de :01 falló y se cambió de dirección para seguir. No hay «k de n» para CE-2, como sí lo hay para CE-1 y CE-3.
3. **E2 · REQ-02 no es unívoco.** Dice «emparejamiento seguro por confirmación» (`parcela.md:46`). Lo medido es otra cosa: Android declara IO 0x01 y autenticación 0x03 (`prueba-real.txt:58`); el periférico contesta sin entrada ni salida, 0x03, con bonding general sin MITM, 0x04 (`GestorDeSeguridad.cs:15,18`); la clave queda de tipo 4 (`prueba-real.txt:60`). Según la especificación Core, la clave de tipo 4 es no autenticada (C: NO VERIFICADO aquí). «Seguro» admite dos lecturas: socket seguro o clave autenticada.
4. **E2 · TS-2 no es atómica.** «Puede diferir del real» (`intake.md:65`) mezcla cuatro diferencias:
   - (a) el método: SSP frente a PIN 0000 heredado; RootCanal ignora el PIN (`Medios…md:58`);
   - (b) el diálogo de Android;
   - (c) el tipo de clave;
   - (d) el registro SDP, que no está medido (D4).

   Cada una necesita su propia medición en la segunda etapa.
5. **E2 · «Espacio de red del contenedor del emulador» admite dos lecturas** (ADR:27):
   - dentro del contenedor del emulador (`docker exec`): lo medido (`prueba-real.txt:17-19`);
   - en un contenedor aparte con `--network container:`: lo que pide el intake (`intake.md:50`) y no está medido (LAZ-0005).
6. **E2 · El disparador de reemplazo no es atómico** (ADR:33: «si falla en S2, S3 o S5»):
   - omite S6b, la dirección fija que da título al ADR, y S4;
   - apunta a una prueba corta local, sin publicar y sin juzgar, que el propio ADR excluye como evidencia (ADR:23).

   Hoy el sustento publicado es la evidencia de PAR-PTE-03.
7. **E2 · Hay una transferencia sin declarar.** `prueba-real.txt:190` registra `CIERRE conexion=1 bytes=65536` con un hash que no aparece en ningún `SENT` ni en ningún `IGUAL`. No consta si fue un calentamiento o un intento descartado. Además, la agrupación del contrato, «3 ticket 1 IGUAL», junta los 5 envíos con los 2 reinicios: son 12 líneas `IGUAL` (E1: `grep -c`).
8. **E2 · CE-3 se cumple como está escrito, pero no de punta a punta.** Los 5 tickets son el mismo archivo sintético, con el mismo SHA (`prueba-real.txt:98-119`), y «NO es salida real de la librería» (`Prueba-Corta.md:22`). La app usada es la Java mínima, no MotorDsl (`Prueba-Corta.md:11`).
9. **E2 · El presupuesto no se puede verificar.** El intake fija «sobre 2,5 millones de tokens se vuelve a la persona» (`intake.md:50`). No hay registro de consumo en `cdd/`: `grep tokens` sólo devuelve ADR:21 (E1).
10. **E2 · El orden está invertido.** DEC-001 convoca la mesa «antes de la primera parcela de la épica» (`DEC.md:7`), y PAR-PTE-03 ya está `cerrada`. Hay que asentarlo como desvío en la decisión.
11. **E2 · El cierre afirma de más.** `parcela.md` (en `9054249`) dice «D1 (K2) la decidió una mesa» y cita `evidencia/2026-11-27-auditoria.md`. Ese archivo no existe: en `evidencia/` hay 5 archivos, sin auditoría (E1: `ls`).
12. **E2 · La versión de netsim no está fijada.** El ADR cita «may still be evolving» (ADR:22) y sólo se probó `emulator` 37.2.12 / API 37 (`prueba-real.txt:7`). La decisión no declara para qué versión vale.
13. **C → pregunta.** Si el toque en «Pair» llega tarde, Android queda trabado (hallazgo 1). ¿Hace falta un requisito de recuperación (desvincular o rotar la dirección), o queda fuera de alcance?

## Qué falta para decidir
- Fijar el commit juzgado y corregir el cierre de la parcela (hallazgos 11 y 1).
- Declarar o explicar la transferencia sin `SENT` (hallazgo 7).
- Reformular CE-2 y REQ-02 en términos medibles (hallazgos 1-3).
- Asentar el consumo de tokens frente al umbral de 2,5 M (hallazgo 9).
- Elegir una lectura del contenedor, o dejarla atada a LAZ-0005 con un efecto si falla (hallazgo 5).

## P3 · Texto propuesto (ADR-0004 §3 y §4)
**§3 Decisión.**
- **TS-3:** A. Transporte propio en C# por el gRPC de netsim, con dirección fija pasada en `ChipInfo`.
  - B queda fuera por la restricción firmada (intake §6). Reabrirla es un retorno L4 a la persona.
  - C queda descartada: por HCI TCP la dirección cambia y el vínculo se rompe (prueba corta, S6a).
  - Sustento: la evidencia de PAR-PTE-03 en el commit <fijar>.
- **TS-2:** se acepta para la 1.0 el emparejamiento SSP con consentimiento sobre netsim. Diferencias conocidas con la 58HB6 real, a medir en la segunda etapa: (a) el método (SSP o PIN 0000), (b) el diálogo, (c) el tipo de clave, (d) el registro SDP. RootCanal no valida el PIN heredado.
- **Vale para:** `emulator` 37.2.12, Android 17 / API 37, y el periférico dentro del contenedor del emulador. El contenedor aparte se rige por LAZ-0005.

**§4 Consecuencias.**
- Pasa a `reemplazado` y vuelve a la persona si alguna de estas pruebas sobre la versión declarada falla:
  - descubrimiento 3 de 3;
  - emparejamiento con `state=12` seguido de RFCOMM abierto;
  - SHA-256 igual 5 de 5;
  - reconexión sin reemparejar tras reiniciar el periférico;
  - o el contenedor aparte de LAZ-0005.
- CE-2 suma la condición «RFCOMM abre después del vínculo».
- Sigue NO VERIFICADO de punta a punta con MotorDsl.Bluetooth.
- Riesgos del intake §10 sin cambio.

## Lo que revisé y está bien
- Hay trazas reales de cada criterio CE-1..CE-3 contra REQ-01..03 y sus pruebas (`parcela.md:44-64`).
- Las seis mutaciones quedan en rojo y cada una cae en la prueba de su REQ (`mutacion.txt`).
- La dirección fija se mantiene tras 2 reinicios (`prueba-real.txt:123-142`), igual que S6b (`Prueba-Corta.md:24`).
- La causa probable del primer fallo está rotulada NO VERIFICADO (`prueba-real.txt:47`), y el desvío de red está medido y declarado (`prueba-real.txt:11-19`).
- El corte por pings de HTTP/2 se documentó, y el código ya no los manda (E1: `grep Ping|KeepAlive` → 0).
- La evidencia enmascara las direcciones de Android.

**NO VERIFICADO:** los logs de `spike/` (fuera de los repositorios), la captura del diálogo, la pcap y el binario del SHA citado.
