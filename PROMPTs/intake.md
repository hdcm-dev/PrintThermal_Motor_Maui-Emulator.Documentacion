# Intake del producto: PrintThermal.Emulator

| Campo | Valor |
|---|---|
| versión | 1.0 |
| estado | borrador |
| fecha | 2026-11-27 |
| framework de destino | IA.CDD 0.15.8 (`b609a2a`) |

## 1. Procedencia

`procedencia: agente` · `autor: agente entrevistador` · `fecha: 2026-11-27` · `planteo: 1.0` · `integrador: 1.0`

## 2. Problema

La persona no dispone de un emulador de la impresora para sus pruebas (I:15).

## 3. Destinatarios

Quien prueba la impresión en el emulador de Android, en local o en pruebas de extremo a extremo (I:15, I:21). Decide el Product Owner (I:3). Mantenimiento: sin dato (PA-5).

## 4. Producto imaginado

Una impresora 58HB6 emulada según especificaciones, que el emulador de Android descubre y empareja (I:15), y que entrega la imagen del ticket (I:21) en PNG (R:12), con interfaz para pruebas automáticas (R:14).

## 5. Objetivo de esta etapa

Verificar con la prueba corta S0-S8 que el medio emulado permite descubrir, emparejar e imprimir (X:12) y, si pasa, imprimir un ticket y obtener su imagen (I:21).

## 6. Restricciones y antiobjetivos

- Producto en .NET 10 (I:21); Bumble sólo en la prueba corta (R:15).
- Descargas sólo dentro de contenedores (R:15).
- Repositorios públicos (I:27).
- Fuera de la primera etapa: inyección de fallos y calibración con la impresora física (R:14).

## 7. Fuentes

| Cita | Archivo (raíz `PROMPTs/`) |
|---|---|
| I:n | `SDD/01-Analisis-Idea-Inicial/Idea-Inicial.md` |
| R:n | `SDD/01-Analisis-Idea-Inicial/OUTPUTs/Respuestas-A-Preguntas.md` (agente en rol) |
| X:n | `00-Fase-Previa/01-Relevamiento/OUTPUTs/Extracto-Analisis-Previos.md` (extracto redactado de análisis locales) |

## 8. Tecnología

.NET 10 (I:21). Contenedor aparte unido a la red del contenedor del emulador (R:13, X:10). Bluetooth Classic, RFCOMM, perfil de puerto serie (X:7). Pila propia en C# después de la prueba corta; sobre 2,5 millones de tokens se vuelve a la persona (R:15). Licencia MIT (R:11).

## 9. Criterios de éxito

| ID | Criterio | Medida |
|---|---|---|
| CE-1 | Descubrimiento desde Android | aparece en 30 s o menos, 3 de 3 (X:13) |
| CE-2 | Emparejamiento | la impresora figura vinculada en Android (X:14) |
| CE-3 | Integridad de lo impreso | huella recibida igual a la enviada, 5 de 5 (X:15) |
| CE-4 | Salida | un PNG por ticket (R:12) |

## 10. Riesgos

- El medio emulado no está verificado de punta a punta (X:9).
- El emparejamiento emulado puede diferir del real (TS-2).
- Fidelidad no calibrada sin medir la impresora física (R:18).

## 11. Preguntas abiertas

| ID | Pregunta | Dueño |
|---|---|---|
| TS-1 | «Campo cercano»: «Dispositivos cercanos» o NFC (PA-1); la mesa no opinó | PO |
| PA-2 | Versión de Android a cubrir | PO |
| PA-3 | Medición de la impresora física | PO |
| TS-4 | Fidelidad sin medición | PO |
| PA-5 | Quién mantiene | PO |
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

## 14. Aprobación

Pendiente de la persona: firma K3, sin plazo ni default. El mandato de delegación no la cubre.

## 15. Control de cambios

| Versión | Fecha | Cambio | Clase |
|---|---|---|---|
| 1.0 | 2026-11-27 | Creación desde el integrador 1.0 | — |
