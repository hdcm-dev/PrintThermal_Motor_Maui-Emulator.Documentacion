# Intake del producto: PrintThermal.Emulator

| Campo | Valor |
|---|---|
| versión | 1.2 |
| estado | aprobado |
| fecha | 2026-11-27 |
| framework de destino | IA.CDD 0.15.8 (`b609a2a`) |

## 1. Procedencia

`procedencia: agente` · `autor: agente entrevistador` · `fecha: 2026-11-27` · `planteo: 1.1` · `integrador: 1.1`

## 2. Problema

La persona no dispone de un emulador de la impresora para sus pruebas (I:15). Tiene que reproducir el caso del equipo con Android 17 (Q:20).

## 3. Destinatarios

Quien prueba la impresión en el emulador de Android, en local o en pruebas de extremo a extremo (I:15, I:21). Decide el Product Owner (I:3). Responsable, la persona; mantenedora durante la primera etapa, la sesión que conduce el emulador (Q2:22).

## 4. Producto imaginado

Una impresora 58HB6 emulada según especificaciones, que el emulador de Android descubre y empareja (I:15), y que entrega la imagen del ticket (I:21) en PNG (R:12), con interfaz para pruebas automáticas (R:14). Se accede a la imagen por una API HTTP de tickets (I:63) con OpenAPI y página Scalar (I:81), y por un visor web sin usuarios, integrado al servicio de la API (I:69, I:75), que la llama por HTTP como punto de prueba y ejemplo (I:87). «Campo cercano» es sólo «Dispositivos cercanos» de Bluetooth (Q:17, Q:31). Se publica en un release de GitHub, con imagen de contenedor de versión fija (Q2:16), y deja un conocimiento de montaje en `Ng.IA-Context.Scene` (I:53, I:55).

## 5. Objetivo de esta etapa

Verificar con la prueba corta S0-S8 que el medio emulado permite descubrir, emparejar e imprimir (X:12) y, si pasa, imprimir un ticket y obtener su imagen (I:21).

## 6. Restricciones y antiobjetivos

- Producto en .NET 10 (I:21); Bumble sólo en la prueba corta (R:15).
- Descargas sólo dentro de contenedores (R:15).
- Repositorios públicos (I:27).
- Fuera de la primera etapa: inyección de fallos y calibración con la impresora física (R:14); la medición de la 58HB6 real va en la segunda, a cargo del agente (Q:22, Q:31).
- Fuera de alcance: NFC, con la puerta abierta (Q:17, Q:31), e iOS, sin Bluetooth emulado (I:51).

## 7. Fuentes

| Cita | Archivo (raíz `PROMPTs/`) |
|---|---|
| I:n | `SDD/01-Analisis-Idea-Inicial/Idea-Inicial.md` |
| R:n | `SDD/01-Analisis-Idea-Inicial/OUTPUTs/Respuestas-A-Preguntas.md` (agente en rol) |
| Q:n | `00-Fase-Previa/01-Relevamiento/OUTPUTs/01-respuestas.md` (respuestas de la persona a la ronda 01, transcriptas por un agente) |
| Q2:n | `00-Fase-Previa/01-Relevamiento/OUTPUTs/02-respuestas.md` (respuestas de la persona a la ronda 02, transcriptas por un agente) |
| X:n | `00-Fase-Previa/01-Relevamiento/OUTPUTs/Extracto-Analisis-Previos.md` (extracto redactado de análisis locales) |

## 8. Tecnología

.NET 10 (I:21). Contenedor aparte unido a la red del contenedor del emulador (R:13, X:10). Bluetooth Classic, RFCOMM, perfil de puerto serie (X:7). Pila propia en C# después de la prueba corta; sobre 2,5 millones de tokens se vuelve a la persona (R:15). Licencia MIT (R:11). API HTTP con OpenAPI y página Scalar (I:81); visor Blazor Interactive Server sin usuarios, en el mismo servicio (I:69, I:75). Release en GitHub con imagen de contenedor de versión fija; compilar al vuelo sólo para desarrollar el emulador (Q2:16, I:55). Compilación en runners de GitHub únicamente, sin runner propio, por ser repositorio público (Q2:18). API de tickets y visor sin autenticación, publicados sólo en la red del contenedor de pruebas; uso en pruebas internas y en la scene para reproducir casos (Q2:20). Cliente HTTP tipado y reutilizable para el visor: supuesto del agente, a decidir en la siembra.

## 9. Criterios de éxito

| ID | Criterio | Medida |
|---|---|---|
| CE-1 | Descubrimiento desde Android | aparece en 30 s o menos, 3 de 3 (X:13) |
| CE-2 | Emparejamiento | la impresora figura vinculada en Android (X:14) |
| CE-3 | Integridad de lo impreso | huella recibida igual a la enviada, 5 de 5 (X:15) |
| CE-4 | Salida | un PNG por ticket (R:12) |
| CE-5 | Acceso | el PNG de un ticket se obtiene por la API HTTP y se ve en el visor (I:63, I:69); medida por fijar en la siembra |

## 10. Riesgos

- El medio emulado no está verificado de punta a punta (X:9).
- El emparejamiento emulado puede diferir del real (TS-2).
- Fidelidad no calibrada sin medir la impresora física (R:18); la medición se hará en la segunda etapa (Q:22).
- Sin runner propio, el riesgo de ejecutar código de terceros en un runner del equipo no existe (TS-5, resuelta en Q2:18).
- API y visor sin autenticación: la exposición se limita por la red de pruebas; si se abren a otras redes, el riesgo vuelve (TS-7, resuelta en Q2:20).

## 11. Preguntas abiertas

| ID | Pregunta | Dueño |
|---|---|---|
| TS-1 | «Campo cercano»: «Dispositivos cercanos» o NFC (PA-1). Respondida en la ronda 01: «Dispositivos cercanos»; NFC fuera (Q:17, Q:31) | PO · respondida |
| PA-2 | Versión de Android a cubrir. Respondida: el emulador de pruebas y Android 17 (Q:20) | PO · respondida |
| PA-3 | Medición de la impresora física. Respondida: sí, en la segunda etapa (Q:22, Q:31) | PO · respondida |
| TS-4 | Fidelidad sin medición. Aceptada la medición en la segunda etapa (Q:22); hasta entonces, sin calibrar | PO · respondida |
| PA-5 | Quién mantiene. Respondida en la ronda 02: la persona responsable; mantenedora la sesión que conduce el emulador en la primera etapa (Q2:22) | PO · respondida |
| TS-5 | Runner propio frente a repositorio público (I:55). Respondida en la ronda 02: sólo runners de GitHub (Q2:18) | PO · respondida |
| TS-6 | Release: imagen de versión fija y compilación al vuelo sólo en desarrollo (I:55). Respondida en la ronda 02: aceptada (Q2:16) | PO · respondida |
| TS-7 | API sin autenticación (el visor es «sin usuarios», I:69). Respondida en la ronda 02: sin autenticación, sólo en la red de pruebas (Q2:20) | PO · respondida |
| PA-4 | Verificación del medio | mesa · diferida: prueba corta · motivo: se responde ejecutando S0-S8 |
| TS-2 | Emparejamiento emulado frente al real | mesa · diferida: siembra · motivo: depende del paso S3 |
| TS-3 | Pila propia frente a puente | mesa · diferida: siembra · motivo: depende de la prueba corta |

PA-6 quedó respondida: producto en .NET 10 (I:21).

## 12. Retornos

| Señal | Vuelve a | Efecto |
|---|---|---|
| L1, L2 sin cambio de problema | Corpus / backlog | Registro LAZ de alcance `corpus` |
| L2 o L4 que cambia problema, destinatarios o tecnología | Este normalizado y el integrador | Minor en ambos; fila en §15; LAZ de alcance `normalizado` |
| L4 que cambia el problema | Además el planteo | Versión nueva del planteo; LAZ de alcance `planteo` |
| Hallazgo de maqueta | Según la matriz del orquestador 08 §4 | LAZ con `origen: maqueta` |

## 13. Trazabilidad

| Sección | Desde |
|---|---|
| §2, §3 | INT §1, §2 |
| §4, §5, §6 | INT §3, §8 |
| §8 | INT §4, §5 |
| §9 | INT §4 |
| §10, §11 | INT §7, §9 |
| Ronda 01 (Q) | INT §3, §4, §7, §8 (F7) |
| Ronda 02 (Q2) | INT §3, §7, §8, §10 (F9) |
| Pedido 7 (A1 a A6) | INT §3, §4, §7, §8, §9 (F1, F8) |

## 14. Aprobación

`aprobado: Fernando 2026-11-27 versión: 1.2 sha256: 86b40e98947511c1d7c4c260f7b944b104e3f85748ddcd46e52ef2e0ca80e442 testimonio: PROMPTs/00-Fase-Previa/01-Relevamiento/OUTPUTs/03-respuestas.md`

## 15. Control de cambios

| Versión | Fecha | Cambio | Clase |
|---|---|---|---|
| 1.0 | 2026-11-27 | Creación desde el integrador 1.0 | — |
| 1.1 | 2026-11-27 | Ronda 01 respondida (PA-1, PA-2, PA-3, TS-1, TS-4) y pedido 7 (API, visor, Scalar, release, conocimiento); TS-5 a TS-7 abiertas; texto cerrado para la K3 | — |
| 1.2 | 2026-11-27 | Ronda 02 respondida (P2 a P5): release con imagen de versión fija, sólo runners de GitHub, API sin autenticación en la red de pruebas, mantenedora la sesión del emulador; TS-5 a TS-7 y PA-5 respondidas; todas las TS-n se conservan; texto cerrado para la K3 de la ronda 03 | — |
