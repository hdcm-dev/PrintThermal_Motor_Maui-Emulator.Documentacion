# Planteo de la idea inicial: PrintThermal.Emulator

> `versión: 1.1` · `fecha: 2026-11-27` · `procedencia: agente` · `persona: fernandofilipuzzi-utn`
>
> Siglas de ruta como en `Inventario-Fuentes.md`. «`I:n` = `../../SDD/01-Analisis-Idea-Inicial/Idea-Inicial.md`», «`R:n` = `../../SDD/01-Analisis-Idea-Inicial/OUTPUTs/Respuestas-A-Preguntas.md`», «`X:n` = `OUTPUTs/Extracto-Analisis-Previos.md`», «`Q:n` = `OUTPUTs/01-respuestas.md`» (respuestas de la persona a la ronda 01, transcriptas por un agente). `R` es respuesta de un agente en rol. El pedido 7 (I:44 a I:88) está también en `OUTPUTs/mandato-requisitos-2026-11-27.md`.

## 1. Problema

La persona no dispone de un emulador de la impresora para sus pruebas: «porque aun no tengo ese emulador» (I:15).

## 2. Para quién

- Usa: quien prueba la impresión en el emulador de Android, en local o en un flujo de pruebas de extremo a extremo (I:15, I:21).
- Decide: el Product Owner (I:3).
- Mantiene: sin dato (PA-5).

## 3. Qué se busca

- Un emulador de la 58HB6 construido según especificaciones, conectado al emulador de Android y emparejado desde él (I:15).
- Obtener como salida una imagen, como foto del ticket (I:21).
- Poder instalarlo en el contenedor de pruebas o usarlo en pruebas de extremo a extremo (I:21).
- Acceder a la imagen: una API HTTP de tickets, pedida como «un endpoint para pillar la imagen» (I:63). supuesto: estado, lista, último, por identificador, comandos crudos, esperar y borrar.
- Un visor web sencillo de los tickets, en Blazor Interactive Server, sin usuarios (I:69), integrado al servicio de la API (I:75).
- Que el visor llame a la API, «un punto de testeo y como ejemplo» (I:87), ofrecido con «podes si queres». supuesto: por HTTP, con cliente tipado reutilizable.
- OpenAPI con la página Scalar, en lugar de Swagger (I:81).
- Un release en GitHub, o construir el contenedor al vuelo: «fijate el mejor modo» (I:55). supuesto: imagen de versión fija; al vuelo sólo en desarrollo.
- Un conocimiento en `Ng.IA-Context.Scene` para que otros monten el emulador (I:53).

## 4. Con qué tecnología

| Pieza | Elección | Fuente |
|---|---|---|
| Producto | .NET 10 | I:21 |
| Instalación | contenedor aparte, unido a la red del contenedor del emulador | R:13 |
| Imagen del ticket | PNG | R:12 |
| Prueba corta del medio | Bumble, sólo para la prueba; después pila propia en C# | R:15 |
| Licencia | MIT | R:11 |
| API de tickets | HTTP; OpenAPI con página Scalar | I:63, I:81 |
| Visor | Blazor Interactive Server, sin usuarios, integrado al servicio de la API | I:69, I:75 |
| Visor frente a la API | la llama por HTTP; cliente tipado reutilizable (supuesto) | I:87 |
| Release | GitHub; imagen de versión fija; al vuelo sólo en desarrollo (supuesto) | I:55 |
| Runner | propio, sólo en etiqueta o disparo manual, por ser público (supuesto); la persona pidió «nuestro runner» | I:55 |
| Conocimiento de montaje | `Ng.IA-Context.Scene`, índice de conocimientos | I:53 |
| Especificación | librería de impresión que consume la 58HB6 | I:21 |

## 5. Lo aprendido en la experiencia actual

- La librería usa Bluetooth Classic, RFCOMM con el perfil de puerto serie y socket seguro (X:7, X:8).
- La factibilidad surge de leer código; no está verificada de punta a punta (X:9).
- Un contenedor aparte no llega al simulador de radio por IP; sí compartiendo la red del emulador (X:10).
- En iOS no se puede emular Bluetooth; la persona no sabe si la causa es Xcode (I:51). La causa: NO VERIFICADO.
- Tras preguntar por qué no NFC, la persona aceptó la propuesta (Q:17, Q:31). El caso se reproduce con Android 17 (Q:20).

## 6. Lo que no es

- La inyección de fallos y la calibración con la impresora física no entran en la primera etapa (R:14); la medición de la 58HB6 real va en la segunda, a cargo del agente (Q:22, Q:31).
- NFC fuera de alcance, con la puerta abierta (Q:17, Q:31). iOS: sin Bluetooth emulado (I:51).
- supuesto: no reemplaza la prueba con la impresora física mientras la fidelidad no esté medida (X:11).

## 7. Preguntas abiertas

| ID | Pregunta | Dueño |
|---|---|---|
| PA-1 | ¿«Campo cercano» es el permiso «Dispositivos cercanos» de Android sobre Bluetooth, o NFC? Respondida: sólo «Dispositivos cercanos» (Q:17, Q:31) | PO |
| PA-2 | ¿Qué versión de Android tiene que cubrir el emulador? Respondida: el de pruebas y Android 17 (Q:20) | PO |
| PA-3 | ¿Se podrá medir la impresora física (nombre, emparejamiento, estados, tablas, códigos, avances)? Respondida: sí, en la segunda etapa (Q:22, Q:31) | PO |
| PA-4 | ¿El medio Bluetooth emulado permite descubrir, emparejar e imprimir? | mesa |
| PA-5 | ¿Quién mantiene el producto? | PO |
| PA-7 | ¿Se aprueba el release con imagen de versión fija y compilación al vuelo sólo en desarrollo? (I:55) | PO |
| PA-8 | ¿Se aprueba el runner propio sólo en etiqueta o disparo manual? (I:55) | PO |
| PA-9 | ¿La API va sin autenticación, como el visor «sin usuarios» (I:69)? | PO |
| PA-6 | La persona preguntó (chat, 2026-11-27, relevado por el flujo): «pense que al emulador lo ibas a construir en .net?». Respuesta: sí, .NET 10 (I:21); Bumble sólo en la prueba corta | quien conduce |

## Qué hace y qué guarda

| D-n | Qué hace o qué guarda | Cita |
|---|---|---|
| D-1 | Se deja descubrir y emparejar desde el emulador de Android | I:15 |
| D-2 | Recibe la impresión y produce la imagen del ticket | I:21 |
| D-3 | Ofrece una interfaz para pruebas automáticas | R:14 |
| D-4 | Ofrece una API HTTP de tickets (operaciones: supuesto) | I:63 |
| D-5 | Muestra los tickets en un visor sin usuarios, integrado a la API, que la llama | I:69, I:75, I:87 |
| D-6 | Publica su descripción OpenAPI con la página Scalar | I:81 |
