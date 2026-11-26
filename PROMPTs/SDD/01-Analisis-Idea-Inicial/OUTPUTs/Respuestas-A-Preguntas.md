# Respuestas a las preguntas previas — por delegación del Product Owner

> Responde un agente (sesión `workspace-dev-cc`), no la persona. Mandato: pedido 6 de [Idea-Inicial.md](../Idea-Inicial.md), del 2026-11-26. La persona puede cambiar cualquiera.

| # | Pregunta | Respuesta | Fundamento |
|---|---|---|---|
| 1 | Nombre del repositorio de código | `PrintThermal_Motor_Maui-Emulator`; solución `PrintThermal.Emulator` | Pedido 5. `PrintThermal` rige sobre la grafía del pedido 3 |
| 2 | Licencia | MIT, en los dos repositorios; el archivo entra con el arranque | La misma de la librería que emula |
| 3 | Formato de la imagen del ticket | PNG | Sin pérdida y legible por cualquier herramienta de pruebas |
| 4 | Modo de instalación | Contenedor aparte, unido a la red del contenedor del emulador Android; el binario publicable queda como opción posterior | Pedido 3: «puede ir bien en contenedor» |
| 5 | Agregados | Entra la interfaz para pruebas automáticas. La inyección de fallos y la calibración con la impresora física quedan para una segunda etapa | Pedido 3: pruebas de extremo a extremo |
| 6 | Descargas y transporte | Se descargan Bumble y los paquetes NuGet de gRPC, sólo dentro de contenedores. Primero una prueba corta con Bumble; después, pila Bluetooth propia en C#. Si supera 2,5 millones de tokens, se vuelve a la persona con la alternativa de dejar Bumble como puente | Pedido 3: .NET 10 |
| 7 | Prefijo de parcelas | `PTE` | Sugerido por la sesión CDD |

**Sin dato, a medir en la impresora física antes de darlo por fiel:** respuestas reales de estado, tablas de caracteres, dibujo de códigos QR y de barras, avances de papel.
