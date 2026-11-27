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

## 7 · 2026-11-27

Seis mensajes seguidos del Product Owner, por chat, en orden (A1 a A6). Literales, sin corregir.

**A1**

~~~text
ok, en ios no podemos emular el bluetooth en ios - no se si el problema es xcode  o que , pero bueno, 

para que lo planifiques, cuando termines el mulador, el montaje del emulador lo podes plasmar en un conocimiento , revisa `/Ng/Ng-IA/Ng.IA-Context.Scene/Knowledges/Index-Knowledge.md` y ve la mejor forma de crear un conocimiento ahí que permita ser llamados por los otros para montar el emulador de forma limpia. 

podes generar un release del proyecto emulador en github, acodate de usar nuestro runner y usarlo el binario para montar el contenedor o la otra forma es que cuando se necesite el emulador se contruya el contenedor y la aplicación al vuelo, fijate el mejor modo
~~~

**A2**

~~~text
si respecta esas normas, si necesitas mejorarlas me decis,

¿y pensaste como se va a poder acceder a la imagen que genere? , le vas a generar algo server html o un endpoint para pillar la imagen,
~~~

**A3**

~~~text
podes agregarle un visor web en blazor interactive server para ver los tickets, sencillo solo un visor sin usuarios,
~~~

**A4**

~~~text
el visor blazor integrado al servicio de la api
~~~

**A5**

~~~text
y sumale scalar , antes era swagger a esa api
~~~

**A6**

~~~text
podes si queres que el visor llame a la api, es un punto de testeo y como ejemplo para hacer mas elevado el dia de mañana
~~~

## 8 · 2026-11-27

Respuesta de la persona a la ronda 03 (bloque D1 de la transcripción `00-Fase-Previa/01-Relevamiento/OUTPUTs/03-respuestas.md`). Su «Claro» responde a la firma del intake 1.2; el resto es un pedido nuevo, el pedido 8. Literal, sin corregir.

~~~text
Claro. Vos podes publicar el contenedor listo para usar. Si querés incluirle un      docascode para que los agentes consulten su uso. Tenemos conocimientos de docasdoc pero sin integración con ia layer
~~~

---

Encargo: hacer la fase previa de CDD sobre esta idea.
