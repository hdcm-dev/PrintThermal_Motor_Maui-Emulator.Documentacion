# Informe · Verificación

Alcance: el contrato y sus fuentes, leídos sin modificar nada. No pude reconstruir ni correr la solución: el entorno no autorizó copiar el código ni ejecutar `dotnet`/`git log`. Por eso lo que figura como E1 es un recuento mío hecho con búsqueda sobre las salidas grabadas, no una corrida nueva. Rutas: `<principal>` y `<documentación>`; `par/` = `<principal>/cdd/parcelas/PAR-PTE-03-Medio-Emulado/`.

## P1 (TS-3) · cómo se prueba cada afirmación

- **V1 · La opción A funciona de punta a punta contra Android API 37 sobre netsim.** E2: `par/evidencia/2026-11-27-prueba-real.txt:21-29` (descubre 3 de 3 en unos 2 s), `:48-60` (state=12), `:70-121` (5 de 5 aleatorios y 5 de 5 ticket) y `:123-142` (2 reinicios sin reemparejar). E1 (recuento): la búsqueda `IGUAL|DISTINTO` sobre ese archivo da 12 IGUAL y 0 DISTINTO; en cada caso el SHA-256 enviado coincide con el recibido.
  - **Nivel:** para quien corrió la prueba es E1; para la mesa es una salida grabada que nadie puede reproducir desde el repositorio. El ejecutable de prueba y la app Java «no versionado» (`:3-6`). Que el binario c437… salga del commit 5952ba9 está NO VERIFICADO.
- **V2 · La opción B también es viable, así que P1 se decide por regla, no por factibilidad.** E2: `<documentación>/…/Prueba-Corta.md:36` («Alternativa b … queda comprobada funcionalmente»). E1 (recuento): `spike/logs/s5.txt` da 10 IGUAL y `s6.txt` da 2. Lo que descarta B es la regla E4 de `intake.md:32` («Bumble sólo en la prueba corta»).
  - Los costos de `Medios-Y-Factibilidad.md:94-95` son una estimación «NO VERIFICADA».
  - El tope de 2,5 M tokens (`intake.md:50`) no tiene medida: en `cdd/` «tokens» sólo aparece en `ADR-0004…md:21`. No hay consumo registrado de A.
- **V3 · La opción C ya fue evaluada y falla para el requisito de dirección fija.** El ADR dice «no evaluado» (`ADR-0004…md:29`). Pero S6a (`Prueba-Corta.md:23`) la probó por HCI TCP: la dirección pasó de …:00 a 05:… y el vínculo se rompió. Es E1 grabado, hecho con Bumble, y concuerda con `Medios…md:65` (`GenerateBluetoothAddress`). Queda abierto, como C, si existe otro modo de fijar la dirección por HCI.
- **V4 · La topología «contenedor aparte» no se probó nunca.** E2: `intake.md:50` y `ADR-0004…md:20` la suponen. Las dos corridas fueron con `docker exec` dentro del contenedor del emulador (`Prueba-Corta.md:9`, `prueba-real.txt:11-19`).
  - Además, el puerto gRPC es aleatorio: 34503 en `Medios…md:23` y 37397 en `prueba-real.txt:13`.
  - `TransporteNetsim.Conectar(Uri …)` (`TransporteNetsim.cs:49`) recibe el destino desde afuera, y `OpcionesPeriferico.cs` no lo descubre.
  - Hay criterio posible (S1 con `--network container:`), pero no se ejecutó.
- **V5 · El arreglo de los pings HTTP/2 no tiene prueba.** E2: netsim cortó el flujo dos veces por los pings (`prueba-real.txt:152,167`). El arreglo está en el código (`TransporteNetsim.cs:26-31`). Ninguna de las 20 pruebas lo fija (`pruebas.txt:17-57`): si alguien reintroduce `KeepAlivePingDelay`, sólo lo detectaría otra prueba real. La corrida limpia duró unos 4 min (15:12:37–15:16:27). Que netsimd se apague solo (`Medios…md:75`) tampoco se probó en real.
- **V6 · A depende de un protocolo no documentado, escrito a mano (D2).** E2: la correspondencia entre la fuente y el binario de netsim está «NO VERIFICADA» (`Medios…md:69`), y la fuente pública advierte «may still be evolving» (`ADR-0004…md:22`). Es un riesgo que corresponde a la sección 4 del ADR, no una refutación.

## Evidencia unitaria y de mutación de PAR-PTE-03 · nivel declarado

- **V7 · El «20 en verde» del contrato no está en ningún commit.** E1: la búsqueda `^\s+Passed ` sobre `pruebas.txt` da 20. Ese archivo, el .trx y `RfcommTests.cs` (con la prueba 20, `UnaDesconexionAMitadDelTicket…`) están modificados sin commit en la rama. En HEAD la evidencia dice «19 de 19 (15 nuevas + 4 del esqueleto)» (diff de `pruebas.txt:1`). Además `tasks.md:11` dice «19 de 19».
- **V8 · Pruebas primero: se cumple para las tres pruebas de los REQ.** E2: `rojo.txt:218-220` (17 en total, 13 en rojo), con las pruebas de REQ en `:50,150,166`. Tres pruebas se agregaron después sin rojo: `ElTransporteHablaGrpc…`, `SinNetsimEscuchando…` y `UnaDesconexion…`. No incumple la regla, porque ninguna es una `prueba:` de REQ, pero conviene declararlo.
- **V9 · Mutación 6 de 6 muertas** (`mutacion.txt:4-21`), contra un controlador y un Android simulados que escribió el mismo agente (`plan.md:28`). Prueban la coherencia interna del código; la interoperabilidad la prueba sólo V1 (`plan.md:36`).
- **V10 · La prueba de REQ-02 compara contra las constantes de D3.** E2: `SeguridadTests.cs:51` exige `0x03, 0x00, 0x04`. Prueba que el código hace lo que dice D3, no que Android lo acepte; eso sale sólo de `prueba-real.txt:52-60`.

## P2 (TS-2) · emparejamiento emulado

- **V11 · Qué emparejamiento se midió.** E2 (`prueba-real.txt:57-60`): Android declara IO 0x01 y autenticación 0x03; el periférico responde NoInputNoOutput; la clave resultante es de tipo 4 (sin autenticar); el diálogo es la variante 3 (consentimiento).
- **V12 · CE-2, tal como está medido, no distingue un vínculo inservible de uno usable.** E2 + E3 (observado):
  - Primer intento con XX:XX:XX:XX:00:01: Android quedó en state=12. En la conexión siguiente nunca hubo «clave de enlace guardada» ni PSM 3, y RFCOMM venció (`:44-47`, `:163-166`).
  - La causa quedó «NO VERIFICADO». Se repitió con otra dirección, no con la misma.
  - Resultado funcional: 1 de 2. Por la medida de CE-2 («figura vinculada», `intake.md:57`): 2 de 2.
  - Propongo endurecer CE-2: «vinculada y primer envío íntegro sin reemparejar».
- **V13 · El PIN heredado no tiene criterio posible en el medio emulado.** E2: RootCanal ignora el PIN (`Medios…md:58`, `legacy_pairing.rs`). El camino existe en el código (`GestorDeSeguridad.cs:63-68`) y sólo tiene prueba unitaria (`SeguridadTests.cs:78-88`).
- **V14 · El cliente de las pruebas no es la librería real.** E2: S4 pedía «una app con MotorDsl.Bluetooth» (`Medios…md:114`). Se usó una app Java con la misma llamada (`Prueba-Corta.md:11`, `prueba-real.txt:6`), así que la librería queda NO VERIFICADA. El diálogo de Samsung queda fuera (`Medios…md:88`). El ticket es «ESC/POS sintético» (`Prueba-Corta.md:22`) y los 5 tickets tienen el mismo hash: la variedad de contenido la aportan sólo los 5 envíos aleatorios.
- **V15 · Las opciones de P2 frente a las reglas.** E4: la medición de la 58HB6 es de la segunda etapa (`intake.md:35`) y TS-4 ya aceptó «sin calibrar» (`intake.md:77`). La opción A de P2 es coherente con eso. La opción B contradice el intake firmado: frenaría la 1.0 por algo que el intake pone fuera de la primera etapa.

## Procedimiento

- **V16 · La precondición de DEC-001 no se cumple al pie de la letra.** E2: DEC-001 pide el resultado de la prueba corta «publicado» y la mesa «antes de la primera parcela» (`DEC.md:7`). La prueba corta sigue «local, no publicada» (`contrato.md:23`), y `ADR-0004…md:23` dice que el ADR «no los usa como evidencia». Si la mesa se apoya en S6a y S5, la sección 1 del ADR tiene que cambiar o hay que publicar la prueba corta.

## P3 · texto propuesto para ADR-0004 (desde Verificación)

> **§3 Decisión.** A: transporte propio en C# sobre el gRPC de netsim con dirección fija. B se descarta por regla (intake §6: «Bumble sólo en la prueba corta»), no por factibilidad: S5 la mostró viable. C se descarta porque por HCI TCP la dirección cambia y rompe el vínculo (S6a). Para la 1.0 se acepta el emparejamiento emulado (SSP con consentimiento, clave sin autenticar). La fidelidad frente a la 58HB6 (SSP o PIN, registro SDP, clase) se mide en la segunda etapa (intake §6, TS-4). Evidencia: la prueba corta S0-S8 (publicada con este ADR) y PAR-PTE-03 (prueba real 12 de 12 IGUAL, 2 reinicios sin reemparejar). La prueba real corrió dentro del contenedor del emulador y con una app Java, no con MotorDsl.Bluetooth.
>
> **§4 Consecuencias.** CE-2 se mide como «vinculada y primer envío íntegro sin reemparejar». El PIN heredado no es validable en RootCanal y queda sin criterio hasta la impresora real. Pendientes con criterio: un contenedor aparte con `--network container:` y el descubrimiento del puerto gRPC; una prueba que impida reintroducir los pings HTTP/2; el apagado de netsimd; y el registro del consumo de tokens frente al tope de 2,5 M. Riesgo: el protocolo de netsim es interno y escrito a mano (D2); si cambia la versión del emulador, se vuelve a correr la prueba real. Vuelve a la persona si la prueba real con MotorDsl.Bluetooth falla.

## Sin criterio posible (hoy)

- **No hay medio emulado donde probarlo:** el PIN heredado contra RootCanal (V13); el emparejamiento y el SDP reales de la 58HB6; el diálogo de Samsung.
- **Hay criterio, pero no se corrió:** el contenedor aparte (V4), la librería real (V14), el consumo de tokens (V2) y la causa del vínculo roto con XX:XX:XX:XX:00:01 (V12, que se puede reproducir tardando más de 30 s en confirmar).

## Lo que revisé y está bien

- Recuentos propios:
  - 20 Passed en `pruebas.txt`.
  - 12 IGUAL y 0 DISTINTO en `prueba-real.txt`.
  - 10 IGUAL en `s5.txt` y 2 en `s6.txt`.
  - Los hashes enviados y recibidos coinciden línea a línea.
- La condición de `ADR-0004…md:33` (que fallen S2, S3 o S5) no se activó.
- La inversión de la dirección hallada en S6b (`Prueba-Corta.md:29`) está fijada por `SeguridadTests.cs:97`.
- CE-1 (≤ 30 s, 3 de 3) se cumple con margen.
- Las mutaciones M1-M6 apuntan a las líneas del REQ que corresponde.
- Las evidencias enmascaran el loopback, el puerto efectivo y la dirección de Android.
