# Informe · Refutador

Alcance: leí el contrato, ADR-0004, el intake 1.2, R:15, el Integrador, la prueba corta, Medios §2-§3, Q (ronda 01), la parcela, `prueba-real.txt`, `mutacion.txt`, el código de `Bluetooth/` y los informes 01-03. No pude correr `git` ni `dotnet` porque el entorno no los autorizó. El estado de la rama lo leí del reflog, como archivo.

## Veredicto

- **P1 = A no cae, pero su fundamento sí, tal como lo escriben las tres comisiones.** Las tres dicen que B queda fuera «por regla». La regla firmada trae su propia condición de reapertura, y nadie la midió. A vale *mientras* esa condición no se cumpla.
- **P2 = A no cae.** Encontré un fundamento más fuerte que el que dieron las comisiones (R6), y también un camino de código muerto (R7).

## Ataques a P1 (TS-3)

- **R1 · E2. B no es una opción cerrada: es el plan alternativo ya firmado.**
  - R:15 dice: «Si supera 2,5 millones de tokens, se vuelve a la persona con la alternativa de dejar Bumble como puente» (`Respuestas-A-Preguntas.md:15`).
  - El Integrador lo acota a la pila: «si la pila supera 2,5 millones de tokens se vuelve a la persona» (`Documento-Integrador.md:19`).
  - Por eso no es cierto que elegir B sea un L4 que cambia la tecnología (`01-requisitos.md:7`). Tampoco que sea sólo un choque con §6 (`03-lector.md` H3, `02-verificacion.md` V2). Lo correcto: la mesa no puede elegir B, pero el disparador de B existe, está firmado y no figura en ningún §4 propuesto como camino hacia B.
- **R2 · E3. Contraejemplo construido sobre el presupuesto.**
  - La estimación de la pila (a) es de 1,5 a 2,5 M tokens (`Medios…md:94`). Su techo coincide con el umbral.
  - La pila no terminó: el host se conecta en PAR-PTE-04 (`parcela.md:30`, D6) y el contenedor aparte se mide en PAR-PTE-05 (`parcela.md:23`, LAZ-0005).
  - No hay ningún consumo registrado: el único registro de «tokens» en `cdd/` es `ADR-0004…md:21`. Lo confirmé por búsqueda; coincide con 01 y 02.
  - Con la estimación en la mitad alta del rango y dos parcelas más de pila, se cruza el umbral sin que nadie lo vea. Hoy la mesa no puede afirmar ni que A está dentro del presupuesto ni que lo superó. A queda **condicional**, y la condición tiene que ir escrita.
- **R3 · E2. C no cae, porque está dominada.**
  - Por HCI TCP netsim deja la dirección vacía y RootCanal la genera (`Medios…md:65`). S6a lo observó (`Prueba-Corta.md:23`).
  - Con la misma pila C#, C es A sin dirección fija: no aporta nada.
  - Salvedad, ya dicha en V16 y H1: S6a sale de una prueba corta que el ADR excluye como evidencia (`ADR-0004…md:23`).
- **R4 · E2. Ninguna comisión juzgó el commit vigente.**
  - El reflog de la rama registra `rebase (finish): … onto 2dfe61c` y deja la punta en `05789b1`. Los commits `5952ba9` y `9054249`, que citan el contrato y los informes, quedaron fuera de la rama (`.git/logs/refs/heads/parcela/PAR-PTE-03:3-5`).
  - Además, `mutacion.txt` tiene cambios sin commit (estado de git al iniciar la sesión). Agrega M7-M10, que matan las pruebas que no tuvieron rojo (`mutacion.txt:23-40`). Eso responde a V8 y a H12, pero no está en ningún commit.
  - Si la evidencia es la misma antes y después del rebase: NO VERIFICADO.
- **R5 · E2. El riesgo principal de A (D2) lo eligió la parcela, no la opción.**
  - R:15 autoriza «los paquetes NuGet de gRPC», y S8 los usó: Grpc.Net.Client 2.85.0 (`Prueba-Corta.md:26`).
  - D2 escribió el protobuf a mano para no sumar dependencias (`parcela.md:26`).
  - V6 lo presenta como propio de A, pero es un K1 reversible. A no cae; el riesgo se reduce.

## Ataques a P2 (TS-2)

- **R6 · E2. El caso que el producto tiene que reproducir no depende del emparejamiento.**
  - La persona pide «reproducir el caso que tenemos, hoy es android 17» (`01-respuestas.md:20`).
  - Sobre ese caso, la reproducción mostró que «la pantalla fija dependía sólo de los permisos Bluetooth» (`01-respuestas.md:57`).
  - Aceptar el emparejamiento emulado no sacrifica ese caso. Este fundamento es más fuerte que «B contradice §6», y ninguna comisión lo usó.
  - El límite está en otro lado: las capas de Samsung quedan fuera (`Medios…md:88`), y eso no es TS-2.
- **R7 · E2 + C. El camino del PIN heredado es inalcanzable contra Android.**
  - El periférico activa SSP: `0x0C56, 0x01 // Write Simple Pairing Mode` (`PerifericoBluetooth.cs:145`).
  - Android también declara capacidades SSP (`prueba-real.txt:57`).
  - En esas condiciones, el «PIN 0000 sólo si heredado» de D3 (`GestorDeSeguridad.cs:63-68`) no se ejecuta nunca. Que la norma Core imponga SSP cuando ambos lados lo soportan: C, NO VERIFICADO aquí.
  - Pregunta para una opción C de P2: si la 58HB6 real empareja por PIN, ¿conviene apagar SSP para reproducir el diálogo del PIN? RootCanal ignora el PIN (`Medios…md:58`, «TODO: handle result»), así que ni siquiera se sabe si completa. Es pregunta, no refutación.
- **R8 · E3. La opción B de P2 no corrige la falla observada.**
  - El vínculo quedó trabado en «AUTHENTICATING» (`prueba-real.txt:44-47`), con 1 de 2 emparejamientos usables. Es una falla del lado emulado y del tiempo del toque.
  - Medir la impresora real no la arregla. Lo que sí sirve es lo que proponen 01 y 02: endurecer CE-2 dentro de A.

## Errores o contradicciones entre informes

- **V7 contra 01 y H11:** V7 dice que el «20» no está en ningún commit. Pero el mensaje de `9054249` incluye «prueba de desconexión a mitad de ticket» (reflog, línea 4), lo que apoya a 01 y H11. Hoy, de todos modos, ese commit quedó fuera de la rama (R4).
- **El Lector** dice «20 … tanto en HEAD como en la copia de trabajo». Ese HEAD era `9054249`, que ya no es la punta.
- **H5:** el título promete «dirección fija», pero nadie la fija hasta PAR-PTE-04. Lo confirmo: `OpcionesPeriferico` no la tiene (E2, lo cita H5; no lo contradigo).

## P3 · Texto propuesto (sobre la base de 01 y 02, con lo que cambia)

> **§3 Decisión.**
> - **TS-3:** A, transporte propio en C# sobre el gRPC de netsim, con dirección fija en `ChipInfo`.
>   - B es el plan alternativo firmado (R:15): no lo elige la mesa; se activa si la pila supera 2,5 M tokens, y entonces vuelve a la persona.
>   - C está dominada: con la misma pila, por HCI TCP la dirección no es fija (S6a).
> - **TS-2:** se acepta para la 1.0 el emparejamiento SSP con consentimiento sobre netsim (clave sin autenticar). El caso a reproducir depende de los permisos, no del emparejamiento (Q, ronda 01). La fidelidad frente a la 58HB6 (método, diálogo, clave y SDP) se mide en la segunda etapa (intake §6, TS-4).
> - **Sustento:** la evidencia de PAR-PTE-03 en el commit `<punta tras el rebase>` y la prueba corta, publicada con este ADR.
> - **Vale para:** emulator 37.2.12 y API 37, con el periférico dentro del contenedor del emulador.
>
> **§4 Consecuencias.**
> - Vuelve a la persona, con B como alternativa, si se cumple cualquiera de estas condiciones:
>   - el consumo registrado de la pila supera 2,5 M tokens; las parcelas de pila asientan su consumo;
>   - falla la prueba real sobre la versión declarada;
>   - falla el contenedor aparte (LAZ-0005).
> - CE-2 se mide como «vinculada y primer RFCOMM íntegro sin reemparejar».
> - El camino del PIN heredado no se alcanza con SSP activo: o se retira, o se declara sin criterio hasta la 58HB6.
> - D2 (protobuf a mano) es revisable a los paquetes NuGet de gRPC autorizados.
> - Siguen sin verificar MotorDsl.Bluetooth y las capas de Samsung.

## Lo que revisé y está bien

- 12 líneas IGUAL y 0 DISTINTO, y cada hash `tx` coincide con su `rx` (`prueba-real.txt:72-142`). La transferencia de la línea 190 no tiene `SENT` (ya señalada por 01).
- Medios fijó la regla de antemano: «S2-S5 bien y S8 bien = seguir con (a)» (`Medios…md:120`), y la prueba corta la cumple. Eso sostiene A.
- La respuesta de IO es NoInputNoOutput y bonding general sin MITM (`GestorDeSeguridad.cs:48`), igual a lo que dice D3.
- El código suma 2406 líneas (E1: `wc -l`), por debajo del rango estimado de 2500 a 4000.
- El código no manda pings de HTTP/2 (E1: la búsqueda `KeepAlive|Ping` da 0).
- El ADR mantiene `gobierno: humano` y `estado: propuesto`.

**NO VERIFICADO:**
- que las pruebas den 20 de 20 en `05789b1` (sin `dotnet`);
- que la evidencia sea igual antes y después del rebase (sin `git`);
- el binario `c437…`;
- los logs de `spike/`;
- la norma privada (`Rules-Decisiones`, `Knowledge-Mesa`).
