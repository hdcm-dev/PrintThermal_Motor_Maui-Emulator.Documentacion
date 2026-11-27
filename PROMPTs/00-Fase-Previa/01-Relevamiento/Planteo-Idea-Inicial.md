# Planteo de la idea inicial: PrintThermal.Emulator

> `versión: 1.0` · `fecha: 2026-11-27` · `procedencia: agente` · `persona: fernandofilipuzzi-utn`
>
> Siglas de ruta como en `Inventario-Fuentes.md`. «`I:n` = `../../SDD/01-Analisis-Idea-Inicial/Idea-Inicial.md`», «`R:n` = `../../SDD/01-Analisis-Idea-Inicial/OUTPUTs/Respuestas-A-Preguntas.md`», «`X:n` = `OUTPUTs/Extracto-Analisis-Previos.md`». `R` es respuesta de un agente en rol.

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

## 4. Con qué tecnología

| Pieza | Elección | Fuente |
|---|---|---|
| Producto | .NET 10 | I:21 |
| Instalación | contenedor aparte, unido a la red del contenedor del emulador | R:13 |
| Imagen del ticket | PNG | R:12 |
| Prueba corta del medio | Bumble, sólo para la prueba; después pila propia en C# | R:15 |
| Licencia | MIT | R:11 |
| Especificación | librería de impresión que consume la 58HB6 | I:21 |

## 5. Lo aprendido en la experiencia actual

- La librería usa Bluetooth Classic, RFCOMM con el perfil de puerto serie y socket seguro (X:7, X:8).
- La factibilidad surge de leer código; no está verificada de punta a punta (X:9).
- Un contenedor aparte no llega al simulador de radio por IP; sí compartiendo la red del emulador (X:10).

## 6. Lo que no es

- La inyección de fallos y la calibración con la impresora física no entran en la primera etapa (R:14).
- supuesto: no reemplaza la prueba con la impresora física mientras la fidelidad no esté medida (X:11).

## 7. Preguntas abiertas

| ID | Pregunta | Dueño |
|---|---|---|
| PA-1 | ¿«Campo cercano» es el permiso «Dispositivos cercanos» de Android sobre Bluetooth, o NFC? Propuesta: lo primero | PO |
| PA-2 | ¿Qué versión de Android tiene que cubrir el emulador? | PO |
| PA-3 | ¿Se podrá medir la impresora física (nombre, emparejamiento, estados, tablas, códigos, avances)? | PO |
| PA-4 | ¿El medio Bluetooth emulado permite descubrir, emparejar e imprimir? | mesa |
| PA-5 | ¿Quién mantiene el producto? | PO |
| PA-6 | La persona preguntó (chat, 2026-11-27, relevado por el flujo): «pense que al emulador lo ibas a construir en .net?». Respuesta: sí, .NET 10 (I:21); Bumble sólo en la prueba corta | quien conduce |

## Qué hace y qué guarda

| D-n | Qué hace o qué guarda | Cita |
|---|---|---|
| D-1 | Se deja descubrir y emparejar desde el emulador de Android | I:15 |
| D-2 | Recibe la impresión y produce la imagen del ticket | I:21 |
| D-3 | Ofrece una interfaz para pruebas automáticas | R:14 |
