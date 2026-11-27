# Bitácora · fase previa

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
