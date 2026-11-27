# Mandato · responder las preguntas de CDD y encargarse del emulador

> `transcribe: agente [cdd-entrevistador, subagente de contexto propio, 2026-11-27]` · `canal: chat` · `original: mensajes del Product Owner por chat del 2026-11-26 (pedidos 6 y 3 de Idea-Inicial.md) sha256: 9eda615d096fa5c88b8e31a7042593313268ba42dc5680f5408d81b93d80d09e`

El primer párrafo del bloque es el pedido 6, literal. El segundo es el pedido 3 en **transcripción redactada**: se reemplazó el nombre de un equipo por «[el host de desarrollo]» porque el repositorio es público; el original queda fuera del repositorio. La huella es la del bloque tal como figura acá, no la del mensaje original.

## 1. Testimonio

~~~text
ok, responde las preguntas de CDD y encargate vos de tener el emulador de la impresora que necesitas, tenes todas las especificaciones de la impresora que estamos usando

ok, para construir el emulador coordina con la sesión CDD, contale tu idea , y que te ayude a preparar los repositorios y redactar la idea inicial y a ejecutar el framework. , hacelo al emulador en .net 10 , la idea es que lo puedas instalar en el contenedor de pruebas o para cuando tengas que hacer las pruebas e2e en workflow o emulación local, creo que puede ir bien en contenedor ,  ahi tenes la carpeta: `/PrintThemal-Emulator` para alojar el repositorio git de la solución y el repositorio auxiliar para el prompting, etc.  que el proyecto sellame PrintThemal.Emulator , coordina las actividades con la sessión CDD y luego cuando tengas ajustado y probado seguis con las pruebas, vas a tener que [el host de desarrollo] para montar los contenedores de emulacion del android y para el desarrollo de este emulador - tenes del proyecto PrintThermal_Motor_Maui todo lo que necesitas para construir las especificaciones de la impresora, la salida puede simplemente una imagen bitmap como si fuera la foto del ticket - estima todo lo que necesites y empeza
~~~

## 2. Alcance

Cubre: responder por delegación las preguntas de la fase previa y encargarse de tener el emulador. No nombra ninguna K3: **no habilita a firmar** el `intake.md` ni la visión. Lo conceptual del ecosistema sigue siendo de la persona.
