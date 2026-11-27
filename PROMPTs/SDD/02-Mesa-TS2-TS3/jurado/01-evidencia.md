# Juez · Evidencia

**Pregunta:** ¿cada hallazgo y cada voto está probado al nivel de ancla que declara? Abrí el contrato, los cuatro informes y las anclas centrales: `prueba-real.txt`, `Prueba-Corta.md` (S6a, S6b), Medios §2.1 y §3, R:15, intake :32, :35 y :57, ADR-0004, LAZ-0005, `TransporteNetsim.cs`, `GestorDeSeguridad.cs`, `PerifericoBluetooth.cs` y git.

**Comprobaciones propias (E1):**
- La rama está en `05789b1`. `5952ba9` y `9054249` no están en ninguna rama, porque un rebase los dejó fuera.
- Entre `9054249` y `05789b1` no cambia nada en `evidencia/` ni en `src/`. Esto resuelve lo que el Refutador (R4) dejó NO VERIFICADO.
- Hay cambios sin commit en `mutacion.txt` y, además, en `MultiplexorL2cap.cs` y `ServidorSdp.cs`. Esos dos no figuraban al empezar la sesión, así que el código cambió mientras la mesa sesionaba.
- El «20 en verde» queda NO VERIFICADO sobre lo que hay hoy: no corrí `dotnet`.

## Votos

- **P1 = A.** Está construida y medida al nivel E2 (grabado): 12 IGUAL y 0 DISTINTO, y 2 reinicios con «clave de enlace guardada» (`prueba-real.txt:72-142`, :262 y :274).
  - B no se descarta por factibilidad. Su disparador firmado (R:15) existe y nadie lo midió, así que A es condicional.
  - C queda dominada. Su ancla, S6a, es un registro local que hoy el ADR excluye (`ADR-0004:23`).
- **P2 = A.** La medición de la 58HB6 está firmada para la segunda etapa (E4: `intake.md:35`, :76-77). B no corrige la única falla observada, el vínculo trabado, que es del lado emulado (R8).

## Hallazgos

| # | Dictamen | Razón desde el ancla |
|---|---|---|
| h1 | procedente | E2 + E3 comprobado. En el primer intento hubo `state=12`, pero la conexión siguiente abrió sólo el PSM 1, sin clave y sin el PSM 3 (`prueba-real.txt:44-47`, :163-166). Con la medida actual de CE-2 (`intake.md:57`) pasa igual. La redacción «primer RFCOMM íntegro» se puede verificar. |
| h2 | procedente | E2 literal: `Respuestas-A-Preguntas.md:15` («…se vuelve a la persona con la alternativa de dejar Bumble como puente»). `grep tokens cdd/` da sólo `ADR-0004:21`: no hay consumo asentado (E1). |
| h3 | procedente, con salvedad | S6a dice «FALLA… dirección 04:..:00 pasó a 05:..:00» (`Prueba-Corta.md:23`). Pero es E2 de una corrida local con Bumble, y Medios:65 es una inferencia que pide «a medir». Sólo vale si la prueba corta se publica con el ADR (V16). Hay que escribir «dominada», no «refutada», porque sigue abierta otra forma de fijar la dirección por HCI (V3). |
| h4 | procedente | LAZ-0005 existe, está `abierto`, tiene destino PAR-PTE-05 y un criterio medible (§4). La versión 37.2.12 / API 37 consta en `prueba-real.txt:7`. El ADR no menciona ninguna de las dos cosas (E1). |
| h5 | procedente en «sin criterio»; C en «no se alcanza» | Comprobado: SSP queda activo (`PerifericoBluetooth.cs:145`), y la corrida terminó con «Simple Pairing Complete» y clave tipo 4. Que el camino del PIN no se ejecute *nunca* depende de la norma Core (C, NO VERIFICADO). El caso 0x16 no escribe en el registro (`GestorDeSeguridad.cs:63-68`), así que la corrida no puede mostrar su ausencia. |
| h6 | procedente | E1: `prueba-real.txt:190` tiene `CIERRE conexion=1 bytes=65536 sha256=29a3…`, a las 15:13:11, sin `SENT` ni `IGUAL` y fuera de las secciones 2 a 5. |
| h7 | procedente, y más fuerte que lo declarado | Ningún informe juzgó la punta vigente. Además hay cambios sin commit en `src/`. El dictamen tiene que fijar `05789b1` más el estado del árbol, o pedir que se haga commit antes de juzgar. |
| h8 | procedente | E1: buscar `Ping\|KeepAlive` en `*.cs` da 0 en las pruebas. El arreglo es la ausencia de una opción en `TransporteNetsim.cs:26-31`, y sólo una prueba real lo detectaría. Alternativa barata: declarar en el §4 la restricción «sin pings de HTTP/2» (H9). |

## Niveles mal declarados en los informes

- **Verificación V7:** dice que el «20» no está «en ningún commit». Eso era cierto en `5952ba9`, pero sí está en `9054249` y en `05789b1`.
- **Lector:** dice «HEAD» y se refiere a `9054249`, que ya no es la punta.
- **Requisitos (hallazgo 1):** un fallo con causa NO VERIFICADA se declara E3, y es correcto que sea E3, no E2.
- **Los tres primeros informes y el contrato:** tratan la prueba real como E1. Para la mesa es E2, porque el binario y la app no están versionados (V1).

NO VERIFICADO: los registros de `spike/`, la norma privada (`Knowledge-Mesa` §5) y las 20 pruebas sobre el árbol actual.

VOTO: P1=A P2=A
