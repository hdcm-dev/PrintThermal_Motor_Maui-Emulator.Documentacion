Leí el contrato y los cuatro informes, y comprobé algunas anclas en las fuentes. Este es el veredicto:

# Juez · Costo-beneficio

**Pregunta:** ¿corregir cuesta menos que el daño de no hacerlo?

**Anclas que comprobé.**
- R:15 dice «si supera 2,5 millones de tokens, se vuelve a la persona con la alternativa de dejar Bumble como puente» (`Respuestas-A-Preguntas.md:15`).
- El primer vínculo quedó en «AUTHENTICATING» y su RFCOMM venció por tiempo (`prueba-real.txt:44-47`).
- Hay un `CIERRE … bytes=65536` sin `SENT` (`prueba-real.txt:190`).
- El periférico activa SSP (`PerifericoBluetooth.cs:145`).
- En `src/…Bluetooth/` no aparecen `Ping` ni `KeepAlive`.
- La rama hoy es `05789b1 → 2cec4b8 → 27867a9`. No es el `5952ba9` que cita el contrato.

**NO VERIFICADO:**
- que las pruebas den 20 de 20 en la punta actual (no corrí `dotnet`);
- la norma privada;
- los logs de `spike/`.

## 1) Votos

- **P1 = A.** Ya está pagada: 2406 líneas, 12 IGUAL y 0 DISTINTO, y 2 reinicios sin reemparejar.
  - B tira ese costo hundido y además exige volver a la persona (R:15).
  - C no ahorra nada: es la misma pila sin dirección fija.
- **P2 = A.** B frena la 1.0 por una medición que el intake pone en la segunda etapa.
  - Tampoco corrige la falla que se vio, el vínculo trabado (R8).
  - El caso a reproducir depende de los permisos, no del emparejamiento (R6).

## 2) Hallazgos

| # | Dictamen | Razón desde costo-beneficio |
|---|---|---|
| h1 | procedente | Cuesta una cláusula en CE-2. Sin ella, CE-2 da «vinculada» con un RFCOMM inservible, que pasó 1 de 2 veces. |
| h2 | procedente | Asentar el consumo cuesta una línea por parcela. Sin eso, el umbral firmado de 2,5 M se cruza sin que nadie lo vea: el techo estimado coincide con el umbral y faltan dos parcelas de pila. |
| h3 | procedente | Cuesta una línea en el ADR. Sin ella, C parece abierta («no evaluado») y se reabre la discusión. Salvedad: S6a sale de la prueba corta no publicada, así que el sustento tiene que quedar citado. |
| h4 | procedente | LAZ-0005 ya existe, y atar el ADR a ella y a una versión cuesta dos líneas. Sin eso, el ADR promete una topología que nunca se midió, y al actualizar el emulador nadie sabe que hay que repetir la prueba real. |
| h5 | procedente | Declararlo cuesta una línea. Sin eso, una prueba unitaria en verde aparenta cubrir el PIN heredado, que con SSP activo es código muerto y que la segunda etapa necesita saber. |
| h6 | procedente | Explicar una línea de evidencia cuesta casi nada. Sin explicación, queda una transferencia que nadie puede reconciliar en una evidencia que se usa como sustento. |
| h7 | procedente | Fijar el commit no cuesta nada. Sin él, el dictamen cae sobre commits que ya no están en la rama tras el rebase. |
| h8 | procedente, no bloqueante | La prueba es barata. Sin ella, una regresión sólo la detecta una corrida real de unos 4 min. Como el servicio reintenta a los 2 s, el daño es moderado: va como pendiente en §4, no como condición de la decisión. |

**VOTO: P1=A P2=A**
