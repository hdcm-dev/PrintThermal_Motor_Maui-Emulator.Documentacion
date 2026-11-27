# Bitácora · arranque

## 2026-11-27 · siembra hasta la visión (sesión CDD, subagente de un flujo)

- Prerrequisitos: `git status --short` del principal y de este repositorio sin salida; Python 3.11.2, git 2.39.5; `cdd.py normalizado PROMPTs/intake.md --exigir-aprobado` PASA (0). la norma CDD 0.15.8, commit `b609a2a`; `git status --short` de la fuente sin salida al empezar y al terminar.
- Principal (`ffca25a`): `AGENTS.md`, `cdd/cdd.lock.md` (producto `PTE`, `inputs: versionados`, `consulta: DocsAsCode-Designing-Specification@<base de conocimientos privada> 1.5 fe51898`), `.github/workflows/cdd.yml` (plantilla sin cambios, `ubuntu-latest`), `cdd/corpus/vision.md` versión 1 sin firmar (sha256 `f5f7f411ec88647d4fcfcb33ddbfdacd3a84b11a1f064331855b000f4acfab1c`), ADR-0001 a ADR-0008, `DEC.md` (DEC-001 a DEC-005), `CHANGELOG.md` y la ronda K3 en `cdd/testimonios/Vision/OUTPUTs/01-preguntas.md` (P1 a P5).
- Pedido 8 recibido: épica `REQ-EPI-Montaje-Y-Uso` y ADR-0007. Candidato `Red-Movil-Problematica` 2.0: no carga (condición sobre fallas de red incumplida; ADR-0006, «Conocimientos que no cargan»).
- TS-2 y TS-3 («diferida: siembra»): destino ADR-0004 `propuesto`; sin mesa en este arranque, porque dependen del resultado juzgado de la prueba corta (DEC-001). Los registros locales de una corrida de la prueba corta no se publicaron ni se usaron como evidencia.
- Las respuestas a las preguntas de la ronda 02 (dónde se publica la imagen, token, costo) van en §3 de la ronda K3, con citas literales de dos páginas oficiales de GitHub abiertas ese día.
- Compuertas en el principal: `ancla --repo` PASA (0); `esqueleto --repo --exigir` PASA (0, «esqueleto: nuevo · campo esqueleto: del lock»); `documental --exigir-indice cdd` PASA (0, 13 archivos); `lazo` PASA (0).
- Detención K3: la visión espera la respuesta de la persona, sin plazo ni default. `ready` no abre parcelas hasta la firma. Pendiente de la persona también la variable y el secreto de la CI (P5): sin ellos la CI de CDD falla al clonar la norma.
- Sin requisitos sembrados: se siembran después de la firma (orquestador 01, paso 4 detiene antes del paso 5).

## 2026-11-27 · firma de la visión, siembra, SPR-01 y PAR-PTE-01 (sesión CDD, subagente de un flujo)

- Fuente de la norma limpia al empezar y al terminar (`git status --short` sin salida); compuertas corridas con una copia de `b609a2a` (`git archive`), con `python3 -I`.
- Firma K3 de la visión 1: testimonio `cdd/testimonios/Vision/OUTPUTs/01-respuestas.md` del principal (persona, transcripción de agente, canal chat; E1 sha256 `ee47ef5a…dfa2`, E2 sha256 `d3dca755…084d`, receta: el bloque con su salto final, sin las cercas). Lectura: E2 es la opción «Construí y publicá la 1.0», cuya descripción dice «Tomo tu pedido como aprobación de la visión con las recomendadas (2A, 3A, 4A, 5B)», frente a la ronda que somete la visión versión 1 con su huella; ninguna opción cambia el texto (`ready --huella-vision`: versión 1, `f5f7f411…ab1c`). `ready` verifica la firma; con la huella alterada en una copia falla («la visión cambió después de la firma»).
- P5 B: `cdd.yml` deja de descargar la norma; las compuertas corren en local y su salida queda acá. Los nombres de repositorios privados se reemplazaron por su rol en los dos repositorios públicos. Quedan dos literales que una compuerta exige: `consulta:` del lock (`ancla`, forma `Alias@<base> <versión> <commit>`) y la fila «framework de destino» de `PROMPTs/intake.md` (`normalizado`, dentro de la huella firmada). `normalizado PROMPTs/intake.md --exigir-aprobado` sigue en PASA (0) después del reemplazo.
- Commits en `main` del principal: `07d938c` (firma, P5 B, siembra: cinco épicas y once historias), `d00f829` (SPR-01: seis parcelas y olas) y la re-planificación de PAR-PTE-01 (REQ-HIS-Cliente-Tipado en `modifica`, `ENTREGA.md` en `estructura:`), que pidió el cierre: «se sumó a 'modifica' en el PR; no estaba en la parcela de la base».
- `ready --contra main`: PASA (0) en las seis parcelas; PAR-PTE-03 queda en `propuesta` por la mesa de TS-2 y TS-3 (ADR-0004). Olas: 1 PAR-PTE-01; 2 PAR-PTE-02 y 03; 3 PAR-PTE-04; 4 PAR-PTE-05; 5 PAR-PTE-06.
- PAR-PTE-01: pruebas en contenedor `mcr.microsoft.com/dotnet/sdk:10.0.403` con turno en el equipo de cómputo (turnos 217 rojo, 218 y 219 verde, 220 mutación; 2 CPU / 4 GB). Auditor refutador en otro contexto (`claude -p`, mismo modelo, garantía reducida): «VEREDICTO: no refutado», con hallazgos menores que se corrigieron antes del PR.
- Compuertas de PAR-PTE-01 en la rama (base `main`): `cierre --parcela` PASA (0); `cierre --pr` PASA (0); `deuda` PASA (0); `documental --exigir-indice cdd/corpus <parcela>` PASA (0, 29 archivos); `ancla --fw <copia>` PASA (0) con dos avisos: «cdd_commit b609a2a no resuelve en ningún repo de la fuente» y «ningún workflow invoca `cdd.py lazo` ni `cdd.py ancla` … (pasa a falla en 0.16.0)». Este último es consecuencia de P5 B y habrá que resolverlo al migrar a 0.16.0.
- PR #1 (https://github.com/hdcm-dev/PrintThermal_Motor_Maui-Emulator/pull/1), cabeza `8e5e1ad`: guarda con techo 1800 s e intervalo 30 s (`ENTREGA.md`); relectura final: abierto, misma cabeza, `mergeable` y `clean`, una corrida (`cdd`, pull_request, 46016179912) en éxito. **Fusionado por el agente** con commit de merge atado a la cabeza: `9dec7ce`. Rama remota borrada y comprobada (404); `main` local al día, `8e5e1ad` alcanzable, rama local borrada.
- Controles del commit de merge `9dec7ce` en `main`: una corrida (`cdd`, push, 46016325233) en éxito. Sigue: PAR-PTE-02 (ola 2; su `ready` pedirá actualizar la huella de REQ-HIS-Compilacion-Verificada a v2).

## 2026-11-27 · PAR-PTE-04: API, visor Blazor, Scalar y cliente tipado (sesión CDD, subagente de un flujo)

- Fuente de la norma (`IA.CDD`, `b609a2a`): `git status --short` vacío al empezar y al terminar. Compuertas con la copia `fw-b609a2a`, `python3 -I`.
- Re-planificación en `main` (`9e5e1d6`), como las de PAR-PTE-02 y PAR-PTE-03:
  - base `9dec7ce`;
  - REQ-HIS-Cliente-Tipado@v2;
  - REQ-HIS-Compilacion-Verificada@v2 en `modifica`, por `Directory.Packages.props`;
  - REQ-05 (cliente) y REQ-06 (escucha local);
  - velocidad completa, con `plan.md` y `tasks.md`.

  `ready --contra origin/main`: PASA (0).
- La ola 3 corrió con la ola 2 abierta, contra un almacén en memoria y una fuente simulada (D4), y el orden de fusión quedó en LAZ-0009. Los LAZ se numeraron 0006 a 0009 porque PAR-PTE-02 toma 0001 y 0002, y PAR-PTE-03 toma 0005.
- K2 D2 (ADR-0003, opción A) y D3 (contrato de la API): mesa ciega con `claude -p`, mismo modelo y otro contexto. Aceptó D3 con cinco cambios, todos aplicados. Las dos van al lote de la Review.
- Pruebas en `mcr.microsoft.com/dotnet/sdk:10.0.403` con turno en el equipo de cómputo (2 CPU / 4 GB):
  - rojo: 29 de 37;
  - verde final: 39 de 39;
  - mutación: 6 de 6 en rojo;
  - escucha: el host publicado escucha sólo en `127.0.0.1:5080`.
- Recorrido en navegador real: Chrome del contenedor de juicio, por el puente de Docker y un túnel. Va a 1440 y 360 px, con los cuatro estados, y la consola sin errores. Dos corridas descartadas:
  - un 404 de favicon;
  - una vuelta a «cargando» tras un error de prerenderizado.
- Auditor refutador (`claude -p`, mismo modelo, otro contexto): ronda 1 «refutado», ronda 2 «refutado». Las dos se respondieron con correcciones o con LAZ. La respuesta a la ronda 2 no se volvió a auditar.
- Compuertas de PAR-PTE-04 sobre la cabeza `5df2082`, con base `origin/main`. PASA (0) en todas:
  - `cierre --parcela` y `cierre --pr`;
  - `documental --exigir-indice`;
  - `ancla`, que avisa que ningún workflow invoca `cdd.py` (DEC-006) y que eso falla desde 0.16.0;
  - `recorrido`, `lazo` y `deuda`.
- PR #4 (https://github.com/hdcm-dev/PrintThermal_Motor_Maui-Emulator/pull/4), cabeza `5df2082`: `clean`, y la corrida `cdd` del pull request (46027779404) en éxito. Sin fusionar: la fusión la hace otra etapa, en orden.

## 2026-11-27 · PAR-PTE-03: Bluetooth Classic propio en C# contra netsim (sesión CDD, subagente de un flujo)

- Fuente de la norma (`IA.CDD`, `b609a2a`): `git status --short` vacío al empezar y al terminar. Compuertas con la copia `fw-b609a2a`, `python3 -I`.
- Re-planificación en `main` (`2dfe61c`):
  - base `9dec7ce`;
  - lee REQ-HIS-Compilacion-Verificada@v2;
  - ADR-0004 sale de `modifica`, porque tiene gobierno humano.
- Código en `src/PrintThermal.Emulator.Bluetooth/`: HCI por el gRPC de netsim (HTTP/2 sin TLS y protobuf a mano, sin paquetes), L2CAP, SDP, SSP y RFCOMM con créditos. Reemplaza a Bumble.
- Pruebas en `mcr.microsoft.com/dotnet/sdk:10.0.403`, con turno en el equipo de cómputo (2 CPU / 4 GB):
  - rojo: 13 de 17, turno 226;
  - verde: 22 de 22, turno 264;
  - mutación: once en rojo, turnos 248, 250, 257 y 263.
- Prueba real: emulador Android 17, API 37, con turno 242 (2 vCPU / 6 GB) en el equipo del emulador, y la app Java mínima.
  - Descubre 3 de 3.
  - Empareja por SSP.
  - SHA-256 igual 10 de 10.
  - Reconecta 2 de 2 sin reemparejar.
  - Desvío medido: netsim escucha sólo en loopback. El periférico corrió dentro del contenedor del emulador (LAZ-0005).
  - Al terminar: contenedor eliminado y turno cerrado.
- Mesa de D1 (K2, TS-2 y TS-3) con `claude -p`, mismo modelo y otro contexto, en `PROMPTs/SDD/02-Mesa-TS2-TS3/`: tres comisiones, refutador y jurado de cinco.
  - Resultado: TS-3 = A y TS-2 = A, 5 de 5.
  - El texto propuesto para ADR-0004 va al lote de la Review.
- Auditor refutador (`claude -p`, mismo modelo, otro contexto):
  - rondas 1 y 2: «refutado», respondidas con correcciones o con LAZ;
  - ronda 3: «no refutado», y sus menores se aplicaron.
- LAZ abiertos: 0005, 0010, 0011 y 0012. Se saltaron de 0006 a 0009, que tomó PAR-PTE-04 en paralelo.
- Compuertas sobre la cabeza `a23ae7f`, todas en 0:
  - `ready --contra origin/main`: PASA;
  - `cierre --parcela` y `cierre --pr`: PASA;
  - `documental --exigir-indice`: PASA;
  - `ancla`: PASA, con el aviso de que ningún workflow invoca `cdd.py` (consecuencia de 5B, falla en 0.16.0);
  - `lazo` y `deuda`: PASA.
- PR #3 abierto y sin fusionar: la fusión va en orden en otra etapa.

## 2026-11-27 · PAR-PTE-02: intérprete ESC/POS a PNG y almacén de tickets (sesión CDD, subagente de un flujo)

- Fuente de la norma (`IA.CDD`, `b609a2a`): `git status --short` vacío al empezar y al terminar. Compuertas con la copia `fw-b609a2a`, `python3 -I`.
- Re-planificación en `main` (`af03a45`): base `9dec7ce` y REQ-HIS-Compilacion-Verificada@v2 en `lee`, por el «I-3 anticipado» de `ready --contra main` (`cierre` lee `lee` de la parcela en la base).
- Vectores dorados: los `.bin` salen de ejecutar los renderers de la librería cliente (`origin/main` `940fa7f`) en `mcr.microsoft.com/dotnet/sdk:10.0.403` con turno; tres corridas del generador dieron bytes idénticos. Matrices QR de referencia de QRCoder 1.8.0 en modo byte (la sobrecarga de texto elige otro modo).
- Pruebas con turno en el equipo de cómputo (2 CPU / 4 GB): rojo 30 de 30 (turno 224); verde final 61 de 61 y 29 mutantes en rojo (turno 266).
- Auditor refutador en otro contexto (`claude -p`, mismo modelo, garantía reducida): tres rondas, «refutado» en las tres; lo señalado se atendió o quedó en LAZ-0001 (fin de ticket sin corte), LAZ-0002 (protocolo sin medir) y LAZ-0003 (licencia de la fuente en la imagen). No se corrió una cuarta ronda.
- Compuertas en la rama (base `main` `9e5e1d6`): `ready --contra main`, `cierre --parcela`, `cierre --pr`, `documental --exigir-indice`, `ancla --fw <copia>`, `lazo` y `deuda`: PASA (0). `ancla` sigue avisando que ningún workflow invoca `cdd.py` (DEC-006).
- PR #2 (https://github.com/hdcm-dev/PrintThermal_Motor_Maui-Emulator/pull/2), cabeza `ad7b415`: CI `cdd` (pull_request, 46031875233) en éxito; `mergeable` y `clean`. No se fusionó: la fusión va en orden en otra etapa.

## 2026-11-27 · Fusión de PAR-PTE-02, 04 y 03; PAR-PTE-05 y release v1.0.0 (sesión CDD, subagente de un flujo)

- Fusiones por conformación automática (`ENTREGA.md` §1), en orden de olas, con revisión refutadora de cada diff y guarda G1-G4 releída antes del merge:
  - PR #2 (PAR-PTE-02): merge `d577191`.
  - PR #4 (PAR-PTE-04): rebase sobre `main`, con el conflicto sólo en el CHANGELOG. Re-planificación en `main` `60eb8a4` (`lee` REQ-HIS-Almacen-De-Tickets@v2). Merge `8c0867b`.
  - PR #3 (PAR-PTE-03): rebase; conflictos en el CHANGELOG y en SPR-01. Re-planificación en `main` `3dd7c6f` (`lee` REQ-HIS-Compilacion-Verificada@v3). Merge `0b8c5b0`.
- PAR-PTE-05: re-planificación en `main` `9e02187`; PR #5, merge `7192bce`. La parcela tiene el detalle en `cdd/parcelas/PAR-PTE-05-Distribucion/`.
  - Imagen (`aspnet:10.0.14-noble-chiseled` por digest), `release.yml` y la conexión del almacén en disco y del medio Bluetooth al host.
  - Pruebas: rojo 9 de 123, verde 131 de 131 y mutación 9 de 10. Todo con turno en el equipo de cómputo (perfil liviano o pesado).
  - Extremo a extremo con turno 274 y puesto de emulador, en modo INFRA: emulador 1 CPU / 5,5 GB, impresora con `--network container:` 1 CPU / 512 MB. `MotorDsl.SampleApp` imprimió 5 de 5. El PNG de la API tuvo la misma huella que el de la carpeta.
  - Auditor refutador (subagente, mismo modelo): dos rondas, las dos refutaron, con respuesta a cada hallazgo. No se corrió una tercera.
  - Compuertas sobre la cabeza `44134f9` contra `main`: `ready`, `cierre --parcela`, `cierre --pr`, `ancla`, `lazo`, `deuda` y `documental` en PASA.
- Release `v1.0.0` (etiqueta sobre `7192bce`): workflow `release` 46041516862 en éxito, con 131 de 131 pruebas.
  - Imagen `ghcr.io/hdcm-dev/printthermal_motor_maui-emulator:1.0.0`, digest `sha256:3bdebce4…62111`.
  - Binario `printthermal-emulator-1.0.0-net10.0.tar.gz` adjunto.
  - La imagen quedó **privada**: un pull anónimo responde «unauthorized». La visibilidad la decide la persona.
- Al cerrar: emulador y periférico bajados, puesto de emulador liberado, turnos 269 a 281 cerrados y sin contenedores propios.
- NO VERIFICADO:
  - el extremo a extremo con la imagen publicada (es privada) y con el receptor final;
  - LAZ-0011, reproducido dos veces: vincular con `createBond` y después conectar deja a Android sin cifrado;
  - la fidelidad contra la 58HB6 física.
- El navegador del servidor MCP del agente no llegó a la red de contenedores. El visor se capturó con Chrome del emulador de Android.


## 2026-11-27 · PAR-PTE-06: documentación de uso como código (sesión CDD, subagente de un flujo)

- Re-planificación por PR propio: PR #6, merge `dd71ee5` (base `7192bce`, `lee` vigentes, REQ-02, D1-D2).
- PAR-PTE-06: PR #7, merge `3b3f3bb`, por conformación automática con la guarda G1-G4 releída antes del merge.
  - `docs/` con índice por tarea, qué es y límites, montaje, emparejar e imprimir, API (curl y cliente tipado), visor y Scalar, diagnóstico, recetas y la ficha de diseño documental (`DocsAsCode-Designing-Specification` 1.5, aplicado condensado). `README.md` la enlaza.
  - La prueba `DocumentacionTests` corre los ejemplos de bash contra el host real con la fuente simulada y contrasta rutas, campos, claves, valores por omisión, imagen, puerto, mensajes de registro, anclas y páginas con el código.
  - Pruebas: rojo 2 de 133 (sin `docs/`), verde 133 de 133 y mutantes 17 de 17. Todo con turno en el equipo de cómputo, perfil liviano.
  - Auditor refutador (mismo modelo, otro contexto): dos rondas, las dos refutaron, con respuesta a cada hallazgo.
  - Compuertas sobre la cabeza `54bf4d5` contra `main`: `ready`, `cierre --parcela`, `cierre --pr`, `documental`, `ancla`, `lazo` y `deuda` en PASA.
- Abiertos: LAZ-0013 (pasos de `docs/` sin medir con la imagen publicada) y LAZ-0014 (imagen privada: la visibilidad la decide la persona).
- SPR-01 queda con todas sus parcelas cerradas; la Review (K3) es de la persona.

## 2026-11-27 · PAR-PTE-07: vincular desde Ajustes y conectar después, con cifrado; visor sin desborde (sesión CDD, subagente de un flujo)

- Re-planificación por PR propio: PR #8, merge `24e034a` (LAZ-0011 y LAZ-0015 especificados; REQ-HIS-Descubrimiento-Y-Emparejamiento v3 y REQ-HIS-Visor-Web v3).
- PAR-PTE-07: PR #9, merge `60d2a3f`, por conformación automática con la guarda G1-G4 releída antes del merge (cabeza `ed6fca9`, una corrida `dotnet` en éxito, `clean`).
  - Diagnóstico: con netsim, la primera conexión tras encender el Bluetooth de Android lleva el manejador 0 y Android atribuye el fin de la vinculación a otro equipo vinculado; el equipo nuevo queda «AUTHENTICATING». La pila propia hacía su parte. Controles: con otro manejador, o sin otros vínculos, Android cifra.
  - Corrección en la pila C# (ADR-0009, aprobada en rol por el mandato F1): reconexión breve tras un vínculo sin cifrar; traza HCI opcional con las claves tapadas.
  - Visor: la tarjeta del ticket se ajusta al ancho (Chrome con emulación de 540 a 205 px y Chrome del emulador de Android).
  - Pruebas: rojo de REQ-01, verde 143 de 143, mutantes 10 de 10, con turno en el equipo de cómputo, perfil liviano.
  - Emulador de Android API 37 con turno y puesto de emulador: camino de Ajustes 3 de 3 cifrados al primer intento de la app, series de 5 de 5 con la misma huella del PNG; vincular conectando 5 de 5 dos veces.
  - Auditor refutador (mismo modelo, otro contexto): la ronda 1 refutó y la ronda 2 sostuvo.
  - Compuertas sobre la cabeza `ed6fca9` contra `main`: `ready`, `cierre --parcela`, `cierre --pr`, `recorrido`, `documental`, `ancla`, `lazo` y `deuda` en PASA.
- Abierto: LAZ-0016 (casos del vínculo sin medir). La imagen publicada con este cambio sale con el próximo release.
