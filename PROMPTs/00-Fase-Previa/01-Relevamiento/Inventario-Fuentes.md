# Inventario de fuentes: PrintThermal.Emulator

Rutas relativas a esta carpeta. Las filas «local» no están publicadas: su cita sólo resuelve en la copia de trabajo.

## 1. Definiciones

Fuente: documento con ruta, citado `F<n>`. Hueco: `HU-<n>`.

## 2. Inventario

| ID | Ruta | Tipo | Qué aporta | Leído | Hueco |
|---|---|---|---|---|---|
| F1 | `../../SDD/01-Analisis-Idea-Inicial/Idea-Inicial.md` | pedido | palabra de la persona; pedidos 1 a 8 | completo | — |
| F2 | `../../SDD/01-Analisis-Idea-Inicial/OUTPUTs/Respuestas-A-Preguntas.md` | decisión (agente en rol) | nombres, licencia, formato, instalación, transporte | completo | HU-2 |
| F3 | `../../SDD/01-Analisis-Idea-Inicial/OUTPUTs/Medios-Y-Factibilidad.md` (local) | estudio | factibilidad y prueba corta S0-S8 | extractos | HU-3 |
| F4 | `../../SDD/01-Analisis-Idea-Inicial/OUTPUTs/Especificacion-58HB6-Desde-La-Libreria.md` (local) | estudio | protocolo que usa la librería | extractos | HU-2 |
| F6 | `OUTPUTs/Extracto-Analisis-Previos.md` | insumo (extracto de F3 y F4) | hechos publicables citados | completo | — |
| F5 | `OUTPUTs/mandato-respuestas-2026-11-26.md` | pedido (transcripción) | alcance de la delegación | completo | — |
| F7 | `OUTPUTs/01-respuestas.md` | respuestas de la persona (transcripción, ronda 01) | campo cercano, versión de Android, medición | completo | — |
| F8 | `OUTPUTs/mandato-requisitos-2026-11-27.md` | pedido (transcripción) | requisitos A1 a A6 (copia del pedido 7 de F1) | completo | — |
| F9 | `OUTPUTs/02-respuestas.md` | respuestas de la persona (transcripción, ronda 02) | release, runner, autenticación de la API, mantenimiento; aprobación de la 1.1 | completo | — |
| F10 | `OUTPUTs/03-respuestas.md` | respuestas de la persona (transcripción, ronda 03) | aprobación de la 1.2; pedido 8 | completo | — |

## 3. Huecos

| ID | Qué falta | Se cierra con |
|---|---|---|
| HU-1 | cerrado en la ronda 01 (F7): «campo cercano» y versión de Android | PA-1, PA-2 |
| HU-2 | comportamiento de la impresora física | PA-3: se medirá en la segunda etapa (F7) |
| HU-3 | verificación del medio Bluetooth emulado | prueba corta (PA-4) |
