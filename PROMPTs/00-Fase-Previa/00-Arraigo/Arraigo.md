# Arraigo · emulador de la impresora térmica 58HB6

> Paso 0 de la fase previa (IA.CDD 0.15.8).

| Campo | Valor |
|---|---|
| fecha | 2026-11-27 |
| quien conduce | agente entrevistador (subagente de un flujo, contexto propio) |
| repos barridos | `PrintThermal_Motor_Maui-Emulator`, `PrintThermal_Motor_Maui-Emulator.Documentacion` |

## 1. Quién trabaja en esto

| Agente o sesión | Expediente o rama | Qué hace | Medido (fecha) | Comando | Vence | Tipo de conflicto |
|---|---|---|---|---|---|---|
| sesión conductora del proyecto | `main` | idea, análisis y respuestas por delegación | 2026-11-27 | `git log --oneline` | — | — |
| agente entrevistador | `main` del complementario | fase previa | 2026-11-27 | esta corrida | — | — |

El espacio no declara carpeta compartida en `AGENTS.md` ni en un lock (no existen en estos repositorios): fichas y tablero, no aplica.

## 2. Qué existe

| Cosa | Estado medido | Fecha | Cómo se midió |
|---|---|---|---|
| Repositorio de la solución | `main` al día; sólo `.gitignore` y `README.md` | 2026-11-27 | `git fetch`, `git status -sb`, `git ls-files` |
| Complementario | `main` al día; prompts, idea inicial y respuestas | 2026-11-27 | ídem |
| Idea inicial | siete pedidos fechados (el 7, del 2026-11-27, con A1 a A6) | 2026-11-27 | `PROMPTs/SDD/01-Analisis-Idea-Inicial/Idea-Inicial.md` |
| Respuestas por delegación | siete filas; agente en rol, no es ronda normada | 2026-11-26 | `PROMPTs/SDD/01-Analisis-Idea-Inicial/OUTPUTs/Respuestas-A-Preguntas.md` |
| Análisis previos (especificación, medios y factibilidad, borrador) | en disco, locales y sin publicar | 2026-11-27 | `.git/info/exclude` |
| Código del emulador y prueba de punta a punta | no existe; nada se ejecutó según los análisis | 2026-11-27 | `git ls-files`; análisis locales |

## 3. Mapa: idea contra lo existente

| # | Cita literal (`ruta:línea`) | Clase | Buscado en (lugares y qué dio) | Estrategia |
|---|---|---|---|---|
| 1 | «es posible con el emulador incluir esa funcionalidad de red bluetooth» (`PROMPTs/SDD/01-Analisis-Idea-Inicial/Idea-Inicial.md:9`) | EJECUTAR | análisis de factibilidad local: factible según código leído, no verificado | prueba corta S0-S8 |
| 2 | «debian tener emulado lo del campo cercano con la versión de android» (`PROMPTs/SDD/01-Analisis-Idea-Inicial/Idea-Inicial.md:15`) | CONSULTAR | idea, respuestas y análisis: sólo interpretaciones de agentes | consulta con propuesta; respondida en la ronda 01 (`01-Relevamiento/OUTPUTs/01-respuestas.md`): sólo «Dispositivos cercanos» |
| 3 | «hacelo al emulador en .net 10» (`PROMPTs/SDD/01-Analisis-Idea-Inicial/Idea-Inicial.md:21`) | EJECUTAR | respuestas, fila 6 | producto en .NET 10; Bumble sólo en la prueba corta |
| 4 | «creo que puede ir bien en contenedor» (`PROMPTs/SDD/01-Analisis-Idea-Inicial/Idea-Inicial.md:21`) | EJECUTAR | respuestas, fila 4 | contenedor aparte en la red del emulador |
| 5 | «la salida puede simplemente una imagen bitmap como si fuera la foto del ticket» (`PROMPTs/SDD/01-Analisis-Idea-Inicial/Idea-Inicial.md:21`) | EJECUTAR | respuestas, fila 3 | PNG |
| 6 | «publicos» (`PROMPTs/SDD/01-Analisis-Idea-Inicial/Idea-Inicial.md:27`) | EJECUTAR | repositorio de código responde sin credencial | redactar todo lo versionado para público |
| 7 | «pero la solución PrintThermal.Emulator» (`PROMPTs/SDD/01-Analisis-Idea-Inicial/Idea-Inicial.md:35`) | EJECUTAR | respuestas, fila 1 | nombres vigentes |
| 8 | «responde las preguntas de CDD y encargate vos» (`PROMPTs/SDD/01-Analisis-Idea-Inicial/Idea-Inicial.md:41`) | EJECUTAR | mandato transcripto en `01-Relevamiento/OUTPUTs/` | citar las respuestas; la firma no está cubierta |
| 9 | «en ios no podemos emular el bluetooth en ios» (`PROMPTs/SDD/01-Analisis-Idea-Inicial/Idea-Inicial.md:51`) | EJECUTAR | pedido 7, A1; análisis locales no cubren iOS | iOS fuera de alcance |
| 10 | «lo podes plasmar en un conocimiento» (`PROMPTs/SDD/01-Analisis-Idea-Inicial/Idea-Inicial.md:53`) | EJECUTAR | índice de conocimientos de `Ng.IA-Context.Scene`: hay conocimientos `Knowledge-SCENE-*`, ninguno monta este emulador | conocimiento de montaje tras el emulador |
| 11 | «podes generar un release del proyecto emulador en github» (`PROMPTs/SDD/01-Analisis-Idea-Inicial/Idea-Inicial.md:55`) | EJECUTAR | pedido 7, A1; repositorio de código sin release | release; modo a criterio del agente, a aprobar en la ronda 02 |
| 12 | «acodate de usar nuestro runner» (`PROMPTs/SDD/01-Analisis-Idea-Inicial/Idea-Inicial.md:55`) | CONSULTAR | repositorio público: la regla del runner propio en repositorios públicos choca con la frase | consulta con propuesta: runner propio sólo en etiqueta o disparo manual; rige la frase hasta la respuesta |
| 13 | «un endpoint para pillar la imagen» (`PROMPTs/SDD/01-Analisis-Idea-Inicial/Idea-Inicial.md:63`) | EJECUTAR | pedido 7, A2 | API HTTP de tickets |
| 14 | «un visor web en blazor interactive server para ver los tickets, sencillo solo un visor sin usuarios» (`PROMPTs/SDD/01-Analisis-Idea-Inicial/Idea-Inicial.md:69`) | EJECUTAR | pedido 7, A3 | visor sin usuarios |
| 15 | «el visor blazor integrado al servicio de la api» (`PROMPTs/SDD/01-Analisis-Idea-Inicial/Idea-Inicial.md:75`) | EJECUTAR | pedido 7, A4 | un solo servicio |
| 16 | «sumale scalar , antes era swagger a esa api» (`PROMPTs/SDD/01-Analisis-Idea-Inicial/Idea-Inicial.md:81`) | EJECUTAR | pedido 7, A5 | OpenAPI con Scalar |
| 17 | «que el visor llame a la api» (`PROMPTs/SDD/01-Analisis-Idea-Inicial/Idea-Inicial.md:87`) | EJECUTAR | pedido 7, A6 | el visor consume la API por HTTP |

## 4. Barrido de estímulos

Medido el 2026-11-27: `git status -sb` en los dos repositorios da `main...origin/main` sin adelanto ni atraso; no hay otras ramas locales en uso para esta corrida ni flujo de CI versionado (`git ls-files`).

### E-1 · Análisis previos sin publicar

- **Estímulo:** `.git/info/exclude` excluye la carpeta `OUTPUTs/` de la idea inicial.
- **Por qué:** los borradores citan repositorios privados e infraestructura.
- **Contexto:** el planteo y el integrador los citan; un clon público no resuelve esas citas.
- **Evaluar:** reversible; publicar sin redactar no lo es.
- **Opciones:** (a) publicar redactados · (b) mantenerlos locales y trasladar los hechos necesarios ya redactados · (c) no hacer nada: las citas quedan sin respaldo público.
- **Mejor opción:** (b): no expone nada y deja los hechos en archivos versionados.
- **Aplicar:** hecho, con evidencia en `PROMPTs/00-Fase-Previa/01-Relevamiento/OUTPUTs/Extracto-Analisis-Previos.md`.

### E-2 · Descargas rotuladas como pendientes

- **Estímulo:** la cabecera de las respuestas dice que las descargas esperan confirmación.
- **Por qué:** las contestó un agente en rol.
- **Contexto:** sin Bumble y gRPC no corre la prueba corta.
- **Evaluar:** reversible (sólo dentro de contenedores); necesita palabra de la persona.
- **Opciones:** (a) tomar la confirmación recibida · (b) volver a preguntar · (c) no hacer nada: la prueba no arranca.
- **Mejor opción:** (a): el encargo del flujo informa que la persona confirmó arrancar el 2026-11-27, con Bumble sólo para la prueba corta.
- **Aplicar:** hecho, con evidencia indirecta registrada en `PROMPTs/00-Fase-Previa/Bitacora.md` (sin cita literal en disco: NO VERIFICADO).

### E-3 · Prueba corta con recursos compartidos

- **Estímulo:** la prueba necesita un emulador de Android propio y aceleración por hardware en un equipo compartido.
- **Por qué:** los recursos los usan también otros trabajos.
- **Contexto:** bloquea la prueba, no la fase previa.
- **Evaluar:** reversible; no se tocan contenedores ni equipos ajenos.
- **Opciones:** (a) correr con turno · (b) correr sin turno · (c) no hacer nada: el medio queda sin verificar.
- **Mejor opción:** (a): evita interferir con otros trabajos.
- **Aplicar:** parado · motivo: fuera del alcance de esta corrida · condición de salida: turno asignado a quien conduce la prueba.

## 5. Salida

- Filas `NO BUSCADO`: 0.
- Estímulos: 2 aplicados · 0 PEDIDO · 0 mesa · 1 parado con motivo y condición de salida.
- Consulta al dueño (fila 2): ¿«lo del campo cercano» es «Dispositivos cercanos» o NFC? Respondida en la ronda 01.
- Consulta al dueño (fila 12): el runner propio en un repositorio público. Va a la ronda 02, con propuesta; sin plazo ni default.
- Avisos al dueño (informativos): ninguno.
- Pedidos: ninguno.
