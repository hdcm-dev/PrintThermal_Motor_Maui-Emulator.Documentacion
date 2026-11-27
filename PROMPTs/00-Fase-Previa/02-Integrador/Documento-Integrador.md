# Documento integrador: PrintThermal.Emulator

> `versión: 1.1` · `fecha: 2026-11-27` · `planteo: 1.1` · `fuentes: F1..F8` (ver `../01-Relevamiento/Inventario-Fuentes.md`; F3 y F4 son locales; F6 es su extracto publicado)

## 1. Problema

[F1] La persona no tiene un emulador de la impresora (`Idea-Inicial.md:15`).

## 2. Destinatarios y roles

[F1] Product Owner decide; quien prueba en local o en flujos usa. Mantenimiento: sin dato.

## 3. Producto y alcance

[F1] Impresora emulada, emparejable desde el emulador de Android, con salida en imagen. [F2] PNG, contenedor aparte, interfaz de pruebas; fallos y calibración, segunda etapa. [F5] La delegación cubre responder y encargarse, no firmar. [F1, F8] API HTTP de tickets (`Idea-Inicial.md:63`); visor Blazor Interactive Server sin usuarios, integrado al servicio de la API (`:69`, `:75`) y que la llama como prueba y ejemplo (`:87`); OpenAPI con página Scalar, en lugar de Swagger (`:81`); release en GitHub o contenedor al vuelo, modo a criterio del agente (`:55`); conocimiento de montaje en `Ng.IA-Context.Scene` (`:53`); iOS sin Bluetooth emulado (`:51`). [F7] «Campo cercano» es sólo «Dispositivos cercanos» de Bluetooth, NFC fuera de alcance; se cubre el emulador de pruebas y Android 17; la medición de la impresora física va en la segunda etapa.

## 4. Tecnología

[F1][F2] .NET 10. [F2] Prueba corta con Bumble y después pila Bluetooth propia en C#; si la pila supera 2,5 millones de tokens se vuelve a la persona. [F3] Ruta propuesta: host mínimo propio (HCI, L2CAP, SDP, RFCOMM) sobre el simulador de radio del emulador, con el transporte separado del dibujo del ticket. Prueba corta S0-S8: arranque con captura, alcance HCI, descubrimiento, emparejamiento, conexión serie, integridad de datos, estabilidad de dirección, versión de Android más nueva y cliente mínimo en .NET. Corte: si fallan el descubrimiento o el emparejamiento, el medio no sirve. Costo estimado (NO VERIFICADO): 0,4 a 0,8 millones de tokens. Propuestas del agente para A1, que la persona aprueba en la ronda 02: release con imagen de contenedor de versión fija; compilar al vuelo sólo para desarrollo; runner propio sólo en etiqueta o disparo manual, por ser repositorio público. Un cliente HTTP tipado y reutilizable para el visor es supuesto del agente (decisión técnica, diferida a la siembra).

## 5. Reglas y datos conocidos

[F4] La librería abre RFCOMM con el UUID de puerto serie y socket seguro; lista sólo dispositivos ya vinculados; envía en trozos de 256 bytes; puede consultar estado y pedir confirmación. El emulador interpreta el camino de imagen y el de texto ESC/POS. Ancho de imagen y columnas reales de la 58HB6: NO VERIFICADO.

## 6. Experiencia actual

[F3] Nada se ejecutó: la factibilidad es de lectura de código. [F4] Sin capturas binarias de referencia en la librería.

## 7. Tensiones

| ID | Fuentes que chocan | Tensión | Dueño |
|---|---|---|---|
| TS-1 | F1 contra F3 | «Campo cercano»: permiso «Dispositivos cercanos» o NFC; sólo hay interpretaciones. Resuelta en la ronda 01 (F7): «Dispositivos cercanos»; NFC fuera, con la puerta abierta | PO · respondida |
| TS-2 | F3 contra F4 | El simulador de radio ignora el PIN: el emparejamiento emulado puede diferir del real | mesa · diferida: siembra · motivo: depende del paso S3 de la prueba corta |
| TS-3 | F1 contra F2 | Bumble no es .NET: queda acotado a la prueba corta; el riesgo de costo de la pila propia tiene el umbral de F2 | mesa · diferida: siembra · motivo: se decide con el resultado de la prueba corta |
| TS-4 | F2 contra F4 | Sin medir la impresora física, la fidelidad no se puede afirmar. La persona aceptó medirla en la segunda etapa (F7); hasta entonces sigue sin calibrar | PO · respondida |
| TS-5 | F1 (A1) contra la regla de repositorio público | La persona pidió usar «nuestro runner»; un runner propio en un repositorio público expone el equipo a código ajeno | PO · se pregunta en la ronda 02 |
| TS-6 | F1 (A1) | Release con binario o contenedor al vuelo: la persona dejó el modo al agente; la propuesta es imagen de versión fija | PO · se pregunta en la ronda 02 |
| TS-7 | F1 (A3, A6) | «Sin usuarios» se dijo del visor; la API no tiene dicho si lleva autenticación | PO · se pregunta en la ronda 02 |

## 8. Decisiones

| ID | Decisión | Estado | Decide |
|---|---|---|---|
| D-01 | Producto en .NET 10 | vigente | persona (F1) |
| D-02 | Repositorios públicos; nombres y solución | vigente | persona (F1) |
| D-03 | PNG, MIT, contenedor aparte, prefijo `PTE` | propuesta | agente en rol (F2); la persona puede cambiarlas |
| D-04 | Bumble sólo en la prueba corta | vigente según el encargo del flujo del 2026-11-27 (NO VERIFICADO literal) | persona |
| D-05 | Pila propia en C# frente a puente permanente | abierta | mesa; vuelve a la persona sobre el umbral |
| D-06 | Android: el emulador de pruebas y Android 17 | vigente | persona (F7) |
| D-07 | NFC fuera de alcance; sólo «Dispositivos cercanos» de Bluetooth | vigente | persona (F7) |
| D-08 | Medición de la impresora física en la segunda etapa, a cargo del agente | vigente | persona (F7) |
| D-09 | API HTTP de tickets; visor Blazor Interactive Server sin usuarios, integrado a la API; Scalar | vigente | persona (F1, F8) |
| D-10 | Release con imagen de versión fija; al vuelo sólo en desarrollo; runner propio sólo en etiqueta o disparo manual | propuesta | agente; la persona la aprueba en la ronda 02 |
| D-11 | Conocimiento de montaje del emulador en `Ng.IA-Context.Scene` | vigente | persona (F1, F8) |

## 9. Riesgos

| ID | Riesgo | Mitigación |
|---|---|---|
| RI-1 | El medio emulado no funciona de punta a punta | prueba corta con corte |
| RI-2 | La pila propia no interopera con Android | referencia con Bumble y capturas |
| RI-3 | Emulador y librería comparten supuestos y todo pasa sin parecerse a la impresora | medir la física; rotular fidelidad no calibrada |
| RI-4 | La dirección Bluetooth cambia y rompe el vínculo (inferencia) | dirección fija (paso S6) |
| RI-5 | Un runner propio ejecuta código de terceros en un repositorio público | sólo en etiqueta o disparo manual (propuesta) |
| RI-6 | API y visor sin autenticación quedan expuestos fuera de la red de pruebas | publicarlos sólo en la red de pruebas (propuesta; se pregunta) |

## 10. Matriz tema por fuente

| Tema | F1 | F2 | F3 | F4 | F5 | F6 | F7 | F8 |
|---|---|---|---|---|---|---|---|---|
| 1 Problema | x | | | | | | | |
| 2 Destinatarios | x | | | | x | | | |
| 3 Producto | x | x | | | x | | x | x |
| 4 Tecnología | x | x | x | | | x | x | x |
| 5 Reglas | | | | x | | x | | |
| 6 Experiencia | | | x | x | | x | x | |

## 11. Control de cambios

| Versión | Fecha | Cambio | Origen (fuente, LAZ-NNNN) |
|---|---|---|---|
| 1.0 | 2026-11-27 | Creación | Inventario |
| 1.1 | 2026-11-27 | Ronda 01 respondida (F7) y pedido 7 (F1, F8): TS-1 y TS-4 respondidas, TS-5 a TS-7, D-06 a D-11, RI-5 y RI-6 | F7, F8 |
