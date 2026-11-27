# Mesa TS-2 y TS-3 · Contrato de entrada

## Índice

1. [Pedido](#1-pedido)
2. [Objeto y fuentes](#2-objeto-y-fuentes)
3. [Paso 0 mecánico](#3-paso-0-mecánico)
4. [Preguntas](#4-preguntas)
5. [Panel, jurado y aplicación](#5-panel-jurado-y-aplicación)

## 1. Pedido

- Literal del intake firmado (§11): «TS-2 | Emparejamiento emulado frente al real | mesa · diferida: siembra · motivo: depende del paso S3» y «TS-3 | Pila propia frente a puente | mesa · diferida: siembra · motivo: depende de la prueba corta».
- DEC-001 (corpus del repositorio principal): la mesa se convoca cuando el resultado de la prueba corta esté publicado, antes de la primera parcela de la épica del medio emulado; destino de TS-2 y TS-3: ADR-0004 (`propuesto`).
- Agregado por quien convoca (PAR-PTE-03, decisión D1, clase K2): la mesa lee además el resultado de la parcela, que construyó la opción A y la probó contra el emulador de Android. Clase K2: decide la mesa con ADR; el PO aprueba en lote en la Review (`Rules-Decisiones.md` §2). ADR-0004 tiene `gobierno: humano`: la mesa propone el texto, no lo aplica.

## 2. Objeto y fuentes

Rutas relativas a los dos repositorios: `<principal>` (rama `parcela/PAR-PTE-03`) y `<documentación>`. Se leen; a los informes no se copian nombres de equipos, IPs ni direcciones Bluetooth completas, porque el expediente es público.

- ADR-0004: `<principal>/cdd/corpus/decisiones/ADR-0004-Transporte-Bluetooth-Classic-Sobre-Netsim.md`
- Intake firmado 1.2 (§6, §8, §10, §11): `<documentación>/PROMPTs/intake.md`
- Prueba corta S0-S8 (local, no publicada): `<documentación>/PROMPTs/SDD/01-Analisis-Idea-Inicial/OUTPUTs/Prueba-Corta.md`
- Medios y factibilidad (§2.1, §3; local): `<documentación>/PROMPTs/SDD/01-Analisis-Idea-Inicial/OUTPUTs/Medios-Y-Factibilidad.md`
- Parcela PAR-PTE-03 y su evidencia: `<principal>/cdd/parcelas/PAR-PTE-03-Medio-Emulado/` (`parcela.md`, `plan.md`, `evidencia/2026-11-27-prueba-real.txt`, `evidencia/2026-11-27-pruebas.txt`, `evidencia/2026-11-27-mutacion.txt`, `evidencia/2026-11-27-rojo.txt`)
- Código: `<principal>/src/PrintThermal.Emulator.Bluetooth/`

## 3. Paso 0 mecánico

`grep -n "TS-2\|TS-3\|Bumble sólo\|Pila propia" intake.md`:

```text
32:- Producto en .NET 10 (I:21); Bumble sólo en la prueba corta (R:15).
50:.NET 10 (I:21). Contenedor aparte unido a la red del contenedor del emulador (R:13, X:10). Bluetooth Classic, RFCOMM, perfil de puerto serie (X:7). Pila propia en C# después de la prueba corta; so
65:- El emparejamiento emulado puede diferir del real (TS-2).
83:| TS-2 | Emparejamiento emulado frente al real | mesa · diferida: siembra · motivo: depende del paso S3 |
84:| TS-3 | Pila propia frente a puente | mesa · diferida: siembra · motivo: depende de la prueba corta |
```

Resultados S0-S8 de la prueba corta (columnas paso | resultado, nombres de equipos reemplazados):

```text
 S0 | OK 
 S1 | OK (con la salvedad de §Entorno) 
 S2 | OK 3/3 
 S3 | OK 
 S4 | OK 
 S5 | OK 5/5 + 5/5 
 S6a | FALLA (esperado) 
 S6b | OK 2/2 
 S7 | OK (todo se corrió ya en API 37.0) 
 S8 | OK 
```

Pruebas de PAR-PTE-03 en verde (`grep -cE "^\s+Passed " evidencia/2026-11-27-pruebas.txt`) y envíos reales (`grep IGUAL|DISTINTO … | sort | uniq -c`):

```text
20
      1 random 1 IGUAL
      1 random 2 IGUAL
      1 random 3 IGUAL
      1 random 4 IGUAL
      1 random 5 IGUAL
      3 ticket 1 IGUAL
      1 ticket 2 IGUAL
      1 ticket 3 IGUAL
      1 ticket 4 IGUAL
      1 ticket 5 IGUAL
```

Rama `parcela/PAR-PTE-03` (`git log --oneline -3`):

```text
5952ba9 PAR-PTE-03: transporte Bluetooth Classic propio en C# (HCI por gRPC de netsim, L2CAP, SDP, SSP, RFCOMM)
77f2f96 PAR-PTE-03: pruebas en rojo del transporte Bluetooth Classic (SDP, SSP, RFCOMM, reintento)
9dec7ce Merge pull request #1 from hdcm-dev/parcela/PAR-PTE-01
```

## 4. Preguntas

- **P1 (TS-3).** ¿Transporte propio en C# sobre el gRPC de netsim (A), puente con un periférico de Bumble (B) o HCI por el puerto TCP de netsim (C)?
- **P2 (TS-2).** ¿Se acepta para la 1.0 el emparejamiento emulado (SSP con consentimiento sobre netsim), sabiendo que el de la 58HB6 real no está medido y que el PIN heredado no se valida en RootCanal? Opciones: A) aceptarlo y dejar la fidelidad del emparejamiento para la medición de la segunda etapa; B) no cerrar la épica hasta medir la impresora real; C) otra, fundada.
- **P3.** Texto propuesto para ADR-0004 (secciones 3 y 4) que el PO aprobaría en la Review.

## 5. Panel, jurado y aplicación

- Comisiones a ciegas, en contextos distintos: Requisitos, Verificación, Lector sin contexto. Refutador al final, después de leerlas. Variables por señal: ninguna citada (descartes: arquitectura, porque la opción A ya está construida y medida; seguridad, porque las claves son de un medio emulado y no salen del contenedor).
- Jurado de cinco contextos distintos (Evidencia, Impacto, Costo/beneficio, Coherencia, Riesgo), mismo modelo que el panel: garantía reducida, declarada.
- Escala de ancla E1-E4 y C (`Knowledge-Mesa` §5). `ciclos_max: 1`.
- Aplica: nadie sobre ADR-0004 (gobierno humano). La salida es un plan: el texto de P3 va al lote de K2 de la Review de SPR-01; la parcela registra D1 con `adr: ADR-0004`.
