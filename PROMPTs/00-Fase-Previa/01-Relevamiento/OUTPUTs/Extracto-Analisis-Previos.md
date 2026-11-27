# Extracto de los análisis previos

> `procedencia: agente`. Sólo los hechos que citan el planteo y el normalizado, redactados para un repositorio público. Los análisis completos quedan locales. Nada se ejecutó: sale de leer código; lo no comprobado es NO VERIFICADO.

## Hechos

- La librería usa Bluetooth Classic, RFCOMM, con el UUID del perfil de puerto serie `00001101-0000-1000-8000-00805F9B34FB`.
- Abre un socket seguro: el emulador tiene que publicar el registro SDP y admitir el emparejamiento previo.
- La factibilidad surge de leer el código del simulador de radio del emulador; descubrir, emparejar e imprimir no está verificado de punta a punta.
- Un contenedor aparte no llega al simulador por IP; sí compartiendo el espacio de red del contenedor del emulador.
- Hay datos que sólo se saben midiendo la impresora física: nombre, emparejamiento, estados, tablas, códigos y avances.
- Prueba corta S0-S8: arranque con captura, alcance HCI, descubrimiento, emparejamiento, conexión serie, integridad, dirección estable, Android más nuevo y cliente mínimo en .NET.
- S2, descubrimiento: la impresora aparece en el escaneo de Android en 30 s o menos, 3 de 3.
- S3, emparejamiento: Android la lista como vinculada.
- S5, integridad: la huella SHA-256 recibida es igual a la enviada, 5 de 5.
