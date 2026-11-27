# Ronda 02 · firma del intake 1.1 y propuestas de publicación

> `fecha: 2026-11-27` · `persona: fernandofilipuzzi-utn` · `entrevistador: agente [cdd-entrevistador, subagente de contexto propio]` · `ronda: 02` · `clase: K3`

## 1. Objetivo de la ronda

Firmar el normalizado y decidir lo conceptual que quedó sin palabra de la persona: el modo de release, el runner y la autenticación de la API. El texto que se firma es el cerrado «intake 1.1 sha256 5a86ed4a70786127ef5c317641c92f3918a656ede410f0e630beeb0821c58ff1» (`PROMPTs/intake.md`). Sin plazo ni default. Si pedís cambios, la versión nueva vuelve para un sí explícito. La respuesta literal va en `../INPUTs/02-respuestas.md`.

## 2. Preguntas

### P1 · ¿Aprobás el intake versión 1.1?
Contexto: sha256 5a86ed4a70786127ef5c317641c92f3918a656ede410f0e630beeb0821c58ff1. Incluye tus respuestas de la ronda 01 y el pedido 7 (API, visor, Scalar, release, conocimiento). TS-2 (emparejamiento emulado frente al real) y TS-3 (pila propia frente a puente) siguen diferidas a la siembra: la mesa no opinó. Quién mantiene el producto (PA-5) sigue abierta. Opciones: A, sí, la versión 1.1; B, no, con los cambios que pidas. Recomendación: A, si las propuestas de P2 a P4 te cierran; si no, respondelas primero y el texto cambia.

### P2 · ¿Cómo se publica el emulador?
Contexto: pediste un release en GitHub y dejaste el modo al agente: «fijate el mejor modo» (Idea-Inicial.md:55). Opciones: A, release con imagen de contenedor de versión fija, y compilar el contenedor al vuelo sólo en desarrollo; B, sólo el binario del release, montado en un contenedor por quien lo usa; C, siempre al vuelo. Recomendación: A: los flujos de prueba usan una versión conocida y repetible, y el desarrollo no espera un release.

### P3 · ¿Dónde corre la compilación del release?
Contexto: pediste usar «nuestro runner» (Idea-Inicial.md:55), pero el repositorio es público: un runner propio que corre código de terceros es un riesgo (TS-5). Opciones: A, runner propio sólo al publicar una etiqueta o por disparo manual, y el resto en runners de GitHub; B, runner propio siempre; C, sólo runners de GitHub. Recomendación: A.

### P4 · ¿La API de tickets lleva autenticación?
Contexto: dijiste «sin usuarios» del visor (Idea-Inicial.md:69); de la API no dijiste nada (TS-7). Opciones: A, sin autenticación y publicada sólo en la red del contenedor de pruebas; B, con una clave simple; C, sin autenticación y abierta a otras redes. Recomendación: A: es una herramienta de pruebas, y la exposición se limita por la red, no por usuarios.

### P5 · ¿Quién mantiene el producto?
Contexto: PA-5, abierta desde el planteo. Opciones: A, vos como responsable y la sesión que conduce el emulador como mantenedora mientras dure la primera etapa; B, otra persona o equipo que nombres; C, dejarla abierta hasta cerrar la primera etapa. Recomendación: A.
