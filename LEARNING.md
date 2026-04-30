# LEARNING — Bitácora maestra del repositorio

Bitácora maestra de aprendizaje en formación técnica de manufactura. No reemplaza ni resume las bitácoras por disciplina — las **conecta**. Aquí escribo lo que ningún archivo individual captura: las relaciones entre disciplinas, los patrones que noto en mí mismo, y las decisiones que tomé sobre cómo construir mi aprendizaje.

> **Voz:** Primera persona, reflexiva. Este archivo es para mí primero. Si un reclutador lo lee, lee mi proceso de pensamiento más que mi currículum técnico.

---

## Cómo navegar este archivo

Si vienes buscando detalle técnico de una disciplina, no es aquí. Es en su LEARNING o README específico:

| Buscas... | Ve a... |
|---|---|
| Detalle técnico de errores y conceptos en CNC | [`2.CNC/LEARNING.md`](./2.CNC/LEARNING.md) |
| Estado y descripción de torno/fresa convencional | [`1.torno-fresado-convencional/README.md`](./1.torno-fresado-convencional/README.md) |
| Estado y descripción de programación CNC | [`2.CNC/README.md`](./2.CNC/README.md) |
| Diseño técnico 2D y proyectos arquitectónicos | [`3.autocad/README.md`](./3.autocad/README.md) |
| Modelado 3D y ensamblajes | [`4.solidworks/README.md`](./4.solidworks/README.md) |
| Certificación oficial Haas | [`5.haas-certification/README.md`](./5.haas-certification/README.md) |

Si vienes buscando **cómo conecta todo entre sí, qué patrones noto en mi forma de aprender, y por qué tomé ciertas decisiones de portafolio** — sigue aquí.

---

## Índice

1. [Conexiones cross-domain](#1-conexiones-cross-domain)
2. [Errores conceptuales que se repiten en distintas disciplinas](#2-errores-conceptuales-que-se-repiten-en-distintas-disciplinas)
3. [Patrones que noto en cómo aprendo](#3-patrones-que-noto-en-cómo-aprendo)
4. [Decisiones técnicas y de portafolio](#4-decisiones-técnicas-y-de-portafolio)
5. [Reflexiones por dominio](#5-reflexiones-por-dominio)

---

## 1. Conexiones cross-domain

Aprendizajes que **no viven en ningún README individual** porque cruzan disciplinas. Los noto porque el repositorio mismo me obliga a pensar las disciplinas en paralelo.

### 1.1 El torno convencional me dio la intuición física que el CNC presupone

Programar CNC sin haber operado un torno manual es posible — pero genera código sintácticamente correcto e industrialmente subóptimo. Cuando programo G01 X20 F100, no pienso solo en "la herramienta se mueve a X=20 a 100 ipm". Pienso en lo que **siente la herramienta** durante ese movimiento: la presión sobre el filo, el calor que genera, la viruta que produce, la vibración del montaje.

Esa intuición se construye operando manualmente. La adquirí durante el curso de torno convencional sin saber que la estaba adquiriendo. Cuando llegué a CNC, ya tenía el modelo mental físico — solo tuve que aprender el lenguaje para comunicárselo a la máquina.

**Implicación práctica para el portafolio:** la dualidad torno convencional + torno CNC no es redundancia. Es una progresión que comunica al reclutador que entiendo el proceso completo, no solo la sintaxis.

### 1.2 La estructura de un programa CNC es la misma que un script de software

Un programa CNC tiene:

1. **Cabecera** con metadata (`(LETRA S - PRODUCCION)`).
2. **Setup** o inicialización (`G21 G17 G40 G49 G80 G90`).
3. **Cuerpo** con la lógica principal.
4. **Cleanup** o finalización (`M05 M30`).

Un script de Python o Node.js tiene exactamente la misma estructura: imports/setup → lógica → cleanup. La función de cada sección es idéntica:

- La cabecera es para que un humano entienda el archivo en 10 segundos.
- El setup garantiza que el estado inicial sea conocido.
- El cuerpo es el trabajo real.
- El cleanup deja el sistema en estado seguro para la próxima ejecución.

Cuando refactoricé el código de la *letra S* de su versión "didáctica" a versión "profesional", apliqué el mismo principio que aplico al refactorizar un controller de Express en mi proyecto `hybridge-blog-api`: separar setup, lógica y cleanup en bloques claros, con comentarios que documenten **intención** (no solo qué hace, sino por qué).

**Implicación:** las habilidades de organización de código son transferibles entre lenguajes G-code y JavaScript. La sintaxis cambia; la disciplina mental no.

### 1.3 La lectura de planos en AutoCAD facilita la programación CNC

No es coincidencia que el curso del CECATI integre AutoCAD junto a torno y CNC. La lectura de planos técnicos es habilidad transversal: el plano es el **input** de toda operación de manufactura.

Antes del curso de AutoCAD, leía planos como un usuario pasivo: identificaba dimensiones y tolerancias. Después de aprender a generarlos en AutoCAD, leo planos como diseñador: entiendo por qué el plano está organizado como está, qué decisiones tomó el dibujante, y dónde podría haber ambigüedades.

Esa lectura activa hace que la traducción **plano → G-code** sea más rápida y precisa. Cuando programé el ejercicio del Caballo en Torno-CNC, identifiqué inmediatamente cuáles cotas eran críticas y cuáles eran de referencia. Sin formación previa en AutoCAD, las habría tratado todas como iguales.

### 1.4 La paciencia del torno se transfiere directamente al maquinado CNC

El torno convencional enseña algo que ningún libro transmite: **el respeto por el material**. Una pasada demasiado profunda destruye la pieza. Una velocidad incorrecta quema la herramienta. El instructor del CECATI dice que "el torno te enseña a ir despacio para llegar más rápido".

Esa misma disciplina aplica al CNC, aunque la máquina ejecute automáticamente. La diferencia es que en torno manual la consecuencia del error es inmediata y visible; en CNC, el error es del programa, pero la consecuencia física llega después con la misma severidad.

**Implicación de carrera:** cuando aplique a vacantes en julio, la combinación "convencional + CNC" no es solo dos disciplinas en mi CV. Es prueba de que internalicé la disciplina mental que la manufactura requiere, no solo el lenguaje técnico.

---

## 2. Errores conceptuales que se repiten en distintas disciplinas

Patrones de error que cometí en una disciplina y luego volví a cometer en otra. Documentarlos aquí me ayuda a **anticiparlos** en disciplinas futuras.

### 2.1 Confundir "memorización" con "comprensión"

**Caso 1: Método I/J en CNC.** Leí sobre I/J en un manual antes de programar. Asumí que comprender la teoría equivalía a poder aplicarla. No: cuando intenté programar, usé I/J como si fuera el radio del arco. La metodología paso a paso solo la internalicé después de cometer el error.

**Caso 2: Comandos AutoCAD complejos.** Conozco conceptualmente qué hace ARRAY o BLOCK. Pero cuando intenté usarlos en el proyecto arquitectónico, descubrí que conocer el comando ≠ saber aplicarlo eficientemente.

**Patrón común:** el cerebro confunde reconocer un concepto con poder ejecutarlo. La diferencia se cierra solo con **práctica deliberada** — escribir la metodología en pasos numerados antes de aplicarla.

**Regla mental adoptada:** antes de afirmar que "domino" un concepto, debo poder enseñárselo a alguien más en pasos numerados. Si no puedo, no lo domino — solo lo reconozco.

### 2.2 Saltarse la verificación previa cuando creo que el trabajo está "obviamente bien"

**Caso 1: Simulación CNC.** He cometido el mismo error tres veces: terminé un programa, tuve confianza, ejecuté sin simular completo, encontré un error que la simulación habría detectado en 30 segundos.

**Caso 2: AutoCAD.** Hice el plano arquitectónico y exporté a PDF sin verificar escala. El PDF salió en escala incorrecta. Tuve que rehacer el setup de impresión.

**Patrón común:** cuando un proceso tiene un paso de "verificación" antes de "ejecución", la confianza alta dispara el impulso de saltar la verificación. El impulso siempre es incorrecto. La verificación existe **precisamente para los casos en que crees que no la necesitas**.

**Regla mental adoptada:** "verificación" no es opcional. Es parte del proceso. Saltarla no es eficiencia — es deuda técnica que se paga con interés.

### 2.3 Parchar errores en lugar de corregirlos en su origen

**Caso 1: Letra S en CNC.** Tenía un arco con I/J incorrectos. En lugar de corregir el arco, agregué movimientos lineales después para "compensar" la geometría errónea. Resultado: código complicado y físicamente incorrecto.

**Caso 2: Probable en código futuro.** No lo he hecho aún en software, pero reconozco el patrón: en lugar de refactorizar una función que está mal, agregar `if`s para tapar los casos donde falla.

**Patrón común:** el costo aparente de "corregir el origen" parece más alto que "compensar el síntoma". Es ilusión: el costo total de los parches acumulados siempre supera el costo del refactor desde el origen.

**Regla mental adoptada:** cuando me encuentro escribiendo "el segundo movimiento es para arreglar lo del primero", paro y vuelvo al primero. La compensación es deuda técnica disfrazada.

---

## 3. Patrones que noto en cómo aprendo

Reflexiones sobre mi propio proceso de aprendizaje. Útiles para diseñar mejores hábitos de estudio.

### 3.1 Funciono mejor con "errores productivos" que con "perfección desde el inicio"

Mi versión inicial de cualquier ejercicio tiene errores. La segunda los corrige. La tercera optimiza. Este patrón **no es defecto** — es cómo funciona la ingeniería real.

Cuando intenté forzar "código perfecto al primer intento", caí en parálisis. Cuando acepté que la primera versión sería imperfecta y mi trabajo era iterar, avancé más rápido y aprendí más profundamente.

**Implicación:** el repositorio refleja esta filosofía. Programas con errores no se borran — se preservan junto a sus correcciones. El error documentado vale más que el código pulido si ningún error precedió al pulido.

### 3.2 Necesito el modelo mental antes de la sintaxis

Cuando aprendí JavaScript con tutoriales que enseñaban sintaxis primero, me sentí perdido. Cuando aprendí leyendo el modelo mental (qué es el event loop, qué es una promesa) y luego la sintaxis, todo encajó.

Lo mismo en CNC: leer la lista de códigos G no me sirvió. Entender que **G-code es un lenguaje que describe trayectorias de una herramienta en un sistema de coordenadas con estado** sí me sirvió. Después de eso, los códigos individuales son detalles.

**Regla mental adoptada:** ante un concepto nuevo, mi primera pregunta es *"¿cuál es el modelo mental?"*, no *"¿cuál es la sintaxis?"*. La sintaxis se memoriza en horas; el modelo mental se construye en semanas.

### 3.3 La conexión cross-domain me consolida más que la repetición dentro de un domain

Repasar cinco veces el mismo concepto de CNC consolida menos que conectarlo a un concepto de software, PLC o gestión. Las conexiones cross-domain crean **redes de significado** en lugar de hechos aislados.

Por eso este archivo (la sección 1) es importante: no es decoración, es la estructura cognitiva que me hace recordar.

**Implicación práctica:** cuando aprenda algo nuevo en cualquier disciplina, dedicar 5 minutos a preguntar *"¿qué de lo que ya sé se parece a esto?"* vale más que 30 minutos de repaso lineal.

---

## 4. Decisiones técnicas y de portafolio

Decisiones explícitas que tomé sobre cómo construir este repo. Documentarlas me obliga a tener razonamiento detrás de las convenciones, no solo costumbre.

### 4.1 Monorepo, no multi-repo

Opté por un solo repositorio (`maquinado`) que contiene las cinco disciplinas, en lugar de un repo por disciplina. Razón: el portafolio comunica una **narrativa unificada de formación técnica**, no cinco proyectos dispersos. Un reclutador abre un link y entiende quién soy en 60 segundos. Cinco links lo dispersan.

Esta decisión es la misma que toman empresas como Google con su monorepo gigante. La lógica subyacente — cohesión narrativa sobre autonomía de módulos — aplica a cualquier escala.

### 4.2 README descriptivo del presente, no aspiracional del futuro

Mi README anterior tenía secciones como "Próximos 2 meses" con 12 items. Si no los cumplía, el README envejecía mal y comunicaba abandono. Lo eliminé.

Regla actual: el README dice **lo que existe ahora** y **un siguiente paso lógico**. Nada más. El "futuro a 2 años" no es información — es deseo.

### 4.3 Convenciones de nomenclatura

- **Carpetas:** kebab-case en español (`ejercicio-cajeado-circular`).
- **Programas G-code:** `Onnnn_descripcion-corta.nc` con número O secuencial estándar FANUC.
- **Fechas en archivos:** `DD-MM-YY` consistente.
- **Commits:** conventional commits con scope (`feat(cnc):`, `docs(torno):`).

Estas convenciones existen porque hace 6 meses no las tenía y mi repositorio era incoherente. Definirlas explícitamente me obligó a aplicarlas con disciplina.

### 4.4 Separación README / LEARNING

Tomé esta decisión recientemente y vale la pena documentarla. **README** describe el estado del trabajo (audiencia: reclutador, voz: tercera persona). **LEARNING** documenta el proceso de aprender (audiencia: yo primero, voz: primera persona).

Mezclarlos era tentador — significaba menos archivos. Pero el contenido sufría: o los READMEs eran demasiado personales para un reclutador, o las reflexiones se perdían en un sea de descripción técnica.

La separación tiene precedentes en cómo trabajan staff engineers profesionales: README pulido para audiencia externa + engineering journal personal para reflexión.

---

## 5. Reflexiones por dominio

Notas breves sobre cada disciplina. **Detalle técnico** vive en sus respectivos LEARNING/README. Aquí solo reflexión.

### 5.1 CNC — la disciplina central de mi proyecto profesional

CNC es el destino. Las otras disciplinas le dan contexto y profundidad, pero la meta es operar y programar máquinas CNC en industria. La certificación Haas en curso refleja esa prioridad.

Lo que he descubierto: programar CNC es 30% sintaxis, 70% pensamiento espacial y planificación de operaciones. La sintaxis se aprende en semanas; el pensamiento espacial se construye con cada ejercicio físico que ejecuto.

Detalle técnico: [`2.CNC/LEARNING.md`](./2.CNC/LEARNING.md).

### 5.2 Torno y fresa convencional — la base física

Esta es la base que el CNC presupone. No es "anterior" en sentido cronológico — es **complementaria** y permanente. Operadores CNC sin formación convencional cometen errores que un torneador clásico identifica en segundos.

Cuando aplique a vacantes mixtas (como Manufacturas Asencio que pide "torno-fresador para herramentales"), esta base es lo que me hace candidato fuerte.

### 5.3 AutoCAD — lectura activa de planos

No es mi prioridad profesional, pero su valor es claro: me hizo lector activo de planos. Esa habilidad es transversal a todo lo demás que hago en manufactura.

### 5.4 SolidWorks — el puente al CAM futuro

SolidWorks es modelado 3D. Pero su valor real para mi trayectoria es como **puente al CAM** (*Computer-Aided Manufacturing*) — la generación automática de G-code desde modelo 3D. Cuando llegue a integrar SolidWorks CAM con CNC, será el momento donde tres disciplinas convergen en una herramienta unificada. Ese momento será un hito de portafolio.

### 5.5 Certificación Haas — credencial industrial reconocida

La certificación oficial Haas no enseña tanto como CECATI — pero **certifica** lo que CECATI enseña con una credencial reconocida globalmente. Es el sello que valida la formación para empleadores que no conocen CECATI.

Detalle técnico: cada módulo aprobado se documenta en [`5.haas-certification/`](./5.haas-certification/).

---

## Próximas entradas esperadas

Cuando ocurran, vendrán nuevas secciones:

- **Primer fallo de programa CNC en máquina real** (vs simulador). La diferencia entre simular y ejecutar va a generar aprendizaje específico.
- **Primera integración SolidWorks CAM → CNC**. El momento donde el modelo 3D se convierte en G-code automáticamente.
- **Primera entrevista técnica de manufactura**. Lo que se preguntó, lo que supe contestar, lo que no.
- **Cuando aprenda alemán técnico**. Ya documentado como meta — el proceso vale registrarlo.

---

**Última actualización:** Abril 2026
**Estado:** Documento vivo. Se nutre cuando algo cruza disciplinas, cuando un patrón se repite, o cuando una decisión merece razonamiento explícito.