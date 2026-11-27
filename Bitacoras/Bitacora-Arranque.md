# Bitácora · arranque

## 2026-11-27 · siembra hasta la visión (sesión CDD, subagente de un flujo)

- Prerrequisitos: `git status --short` del principal y de este repositorio sin salida; Python 3.11.2, git 2.39.5; `cdd.py normalizado PROMPTs/intake.md --exigir-aprobado` PASA (0). IA.CDD 0.15.8, commit `b609a2a`; `git status --short` de la fuente sin salida al empezar y al terminar.
- Principal (`ffca25a`): `AGENTS.md`, `cdd/cdd.lock.md` (producto `PTE`, `inputs: versionados`, `consulta: DocsAsCode-Designing-Specification@IA.Knowledge.Base 1.5 fe51898`), `.github/workflows/cdd.yml` (plantilla sin cambios, `ubuntu-latest`), `cdd/corpus/vision.md` versión 1 sin firmar (sha256 `f5f7f411ec88647d4fcfcb33ddbfdacd3a84b11a1f064331855b000f4acfab1c`), ADR-0001 a ADR-0008, `DEC.md` (DEC-001 a DEC-005), `CHANGELOG.md` y la ronda K3 en `cdd/testimonios/Vision/OUTPUTs/01-preguntas.md` (P1 a P5).
- Pedido 8 recibido: épica `REQ-EPI-Montaje-Y-Uso` y ADR-0007. Candidato `Red-Movil-Problematica` 2.0: no carga (condición sobre fallas de red incumplida; ADR-0006, «Conocimientos que no cargan»).
- TS-2 y TS-3 («diferida: siembra»): destino ADR-0004 `propuesto`; sin mesa en este arranque, porque dependen del resultado juzgado de la prueba corta (DEC-001). Los registros locales de una corrida de la prueba corta no se publicaron ni se usaron como evidencia.
- Las respuestas a las preguntas de la ronda 02 (dónde se publica la imagen, token, costo) van en §3 de la ronda K3, con citas literales de dos páginas oficiales de GitHub abiertas ese día.
- Compuertas en el principal: `ancla --repo` PASA (0); `esqueleto --repo --exigir` PASA (0, «esqueleto: nuevo · campo esqueleto: del lock»); `documental --exigir-indice cdd` PASA (0, 13 archivos); `lazo` PASA (0).
- Detención K3: la visión espera la respuesta de la persona, sin plazo ni default. `ready` no abre parcelas hasta la firma. Pendiente de la persona también la variable y el secreto de la CI (P5): sin ellos la CI de CDD falla al clonar la norma.
- Sin requisitos sembrados: se siembran después de la firma (orquestador 01, paso 4 detiene antes del paso 5).
