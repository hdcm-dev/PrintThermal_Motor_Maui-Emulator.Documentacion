# Idea inicial — emulador de la impresora térmica 58HB6

> Pedidos del Product Owner, literales, fechados y en orden. Canal: chat. Sin interpretación.
> Repositorio público: lo que identificaba infraestructura se reemplazó por un rol entre corchetes (el pedido 3 es por eso una transcripción redactada: se reemplazó el nombre de un equipo; el original queda fuera del repositorio).

## 1 · 2026-11-26

~~~text
estoy especulando, esto vino a cuento con moviles con detección de campo cercano, podria ser esa la causa? en una version de android así? es posible con el emulador incluir esa funcionalidad de red bluetooth y emulación de campo cercano - tal vez necesitariamos construir un software que emule la impresora la 58hb6 y la conectemos virtualmente al emulador de android? esto es factible si tuviesemo esa pieza de software emular la 58hb6?
~~~

## 2 · 2026-11-26

~~~text
para porque aun no tengo ese emulador, - mi idea era simple, era crear ese emulador bajos las especificaciones, vos lo tomabas, lo conectabas al emulador de android, lo emparejabas desde el emulador, y ese equipo emulador debian tener emulado lo del campo cercano con la versión de android -
~~~

## 3 · 2026-11-26

~~~text
ok, para construir el emulador coordina con la sesión CDD, contale tu idea , y que te ayude a preparar los repositorios y redactar la idea inicial y a ejecutar el framework. , hacelo al emulador en .net 10 , la idea es que lo puedas instalar en el contenedor de pruebas o para cuando tengas que hacer las pruebas e2e en workflow o emulación local, creo que puede ir bien en contenedor ,  ahi tenes la carpeta: `/PrintThemal-Emulator` para alojar el repositorio git de la solución y el repositorio auxiliar para el prompting, etc.  que el proyecto sellame PrintThemal.Emulator , coordina las actividades con la sessión CDD y luego cuando tengas ajustado y probado seguis con las pruebas, vas a tener que [el host de desarrollo] para montar los contenedores de emulacion del android y para el desarrollo de este emulador - tenes del proyecto PrintThermal_Motor_Maui todo lo que necesitas para construir las especificaciones de la impresora, la salida puede simplemente una imagen bitmap como si fuera la foto del ticket - estima todo lo que necesites y empeza
~~~

## 4 · 2026-11-26

~~~text
publicos,
~~~

(Respuesta a la visibilidad de los repositorios, en la organización `hdcm-dev`.)

## 5 · 2026-11-26

~~~text
el nombre PrintThermal_Motor_Mauir-Emulator.Documentacion y PrintThermal_Motor_Maui-Emulator.Documentacion - pero la solución PrintThermal.Emulator
~~~

## 6 · 2026-11-26

~~~text
ok, responde las preguntas de CDD y encargate vos de tener el emulador de la impresora que necesitas, tenes todas las especificaciones de la impresora que estamos usando
~~~

---

Encargo: hacer la fase previa de CDD sobre esta idea.
