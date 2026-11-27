# Bitácora · fase previa

## 2026-11-27 · segunda corrida (sesión CDD)

- Ronda 01 versionada (`OUTPUTs/01-preguntas.md`, clase relevamiento, P1 a P3; sin la pregunta de la firma) con su respuesta de la persona, transcripta por un agente del chat (`OUTPUTs/01-respuestas.md`, bloques B1 y B2, sha256 recalculados con la receta de la plantilla). El «Contexto» entre B1 y B2 va rotulado como no testimonio.
- Pedido 7 (A1 a A6) en `Idea-Inicial.md` y como mandato transcripto (`OUTPUTs/mandato-requisitos-2026-11-27.md`; la cabecera lleva la huella del primer bloque, la que lee la compuerta, y la tabla las seis).
- Planteo 1.1, integrador 1.1, arraigo con las filas 9 a 17, intake 1.1 (borrador, texto cerrado). Las TS-1 a TS-4 siguen; TS-1 y TS-4 respondidas; TS-5 a TS-7 nuevas.
- Ronda 02 (K3) emitida en `OUTPUTs/02-preguntas.md`, sin `02-respuestas.md`: la responde la persona.
- Con la ronda 02 abierta, `normalizado` sin `--exigir-aprobado` falla con «la ronda 02 no tiene respuesta registrada»; pasa sobre una copia sin `02-preguntas.md`. Es el mismo caso que se midió con la ronda 01.

## 2026-11-27

- Agente entrevistador (subagente de un flujo). IA.CDD 0.15.8, commit `b609a2a`; la fuente estaba limpia al empezar y al terminar (`git status --short` sin salida).
- Arraigo, planteo 1.0, integrador 1.0 y normalizado 1.0 en borrador. Sin mesas ni subagentes.
- Según el encargo del flujo, la persona confirmó ese día arrancar y usar Bumble sólo para la prueba corta; el producto es .NET. No hay cita literal en disco: NO VERIFICADO.
- Pregunta de la persona relevada por el flujo: «pense que al emulador lo ibas a construir en .net?» (PA-6 del planteo).
- `PROMPTs/SDD/.../Respuestas-A-Preguntas.md` es material de un agente en rol, no una ronda normada.
- K3 sin presentar como archivo: la lleva por chat quien conduce (preguntas en la devolución de esta corrida). Firma pendiente de la persona, sin plazo ni default. Medido: con un `01-preguntas.md` abierto en `OUTPUTs/`, `normalizado` falla con «la ronda 01 no tiene respuesta registrada»; no se dejó versionado. Si la persona responde fuera del chat, la ronda se emite en ese archivo.
- Los análisis completos quedan locales; lo citado se trasladó redactado a `01-Relevamiento/OUTPUTs/Extracto-Analisis-Previos.md`, para que las citas resuelvan en un clon público.

### Salida de las compuertas

Corridas sobre la copia con sólo lo versionado, salvo donde se indica.

| Comando (`cdd.py`) | Resultado | Código |
|---|---|---|
| `arraigo . --exigir-arraigo` | PASA arraigo | 0 |
| `planteo --exigir-producto …/Planteo-Idea-Inicial.md` | PASA planteo | 0 |
| `normalizado PROMPTs/intake.md` | PASA normalizado | 0 |
| `normalizado PROMPTs/intake.md --exigir-aprobado` | FALLA (1): estado 'borrador' | 1, esperado sin firma |
| `esqueleto <principal> --com .` | inerte sin `cdd/cdd.lock.md`; PASA esqueleto (no midió) | 0 |
| `documental PROMPTs README.md` sobre una copia con sólo lo versionado | PASA documental | 0 |
| `documental PROMPTs README.md` sobre la copia de trabajo | FALLA (1): IPv4 en un análisis local, sin publicar | 1 |
