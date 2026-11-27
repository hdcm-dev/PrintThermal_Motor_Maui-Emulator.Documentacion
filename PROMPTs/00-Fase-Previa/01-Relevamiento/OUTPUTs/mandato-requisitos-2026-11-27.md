# Mandato · requisitos nuevos del emulador (pedido 7)

> Insumo transcripto de la fase previa, con la plantilla `mandato.md`. Lo copió un agente del chat; es palabra escrita de la persona.
>
> `transcribe: agente` · `canal: chat` · `original: mensajes del Product Owner por chat del 2026-11-27 (pedido 7 de Idea-Inicial.md, bloques A1 a A6 de §1) sha256: 17e533dc84d9f534f0019ff5c20a5da00ffab7417044043ceb876cde411d64de`

La huella de la cabecera es la del primer bloque (A1), el único que lee la compuerta. Las de los seis bloques, cada una calculada sobre las líneas del bloque con su salto final:

| Bloque | sha256 |
|---|---|
| A1 | 17e533dc84d9f534f0019ff5c20a5da00ffab7417044043ceb876cde411d64de |
| A2 | e1a48a7bea8cda7fdc19fabf8b3bc053a9b23d561205a8d1807d73dbfd805d03 |
| A3 | 1d109afb6562af30e54048a35844680ee95f25c924e0862b1b77ddf90b478382 |
| A4 | 3e26acc0834dff88564571456e2a6dec40b9edeeab78850ace49a6d3d9c25a73 |
| A5 | a4cd827e96dc92dfd055b66fe58de739e9c194d87276e49920c0c7b8edf40f77 |
| A6 | 43675fe623a05aa450cfe369de2e3aeaab74748f271031b89210b09e5397e73c |

## 1. Testimonio

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

## 2. Alcance

Cubre los requisitos A1 a A6: API HTTP de tickets y acceso a la imagen (A2), visor web (A3, A4), Scalar (A5), visor que llama a la API (A6), release y montaje del emulador, y conocimiento reutilizable (A1). No nombra ninguna K3: **no habilita a firmar** el `intake.md`. Lo conceptual del ecosistema sigue siendo de la persona. En A1, la ruta `/Ng/Ng-IA/...` es de un repositorio de conocimientos y no es secreta.
