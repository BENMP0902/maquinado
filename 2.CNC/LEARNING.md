# LEARNING — Programación CNC

Bitácora de aprendizaje de programación CNC. Documento personal donde registro lo que entendí mal, cómo lo corregí, y qué modelo mental me funcionó al final. No es referencia técnica — para eso están los [README de Torno-CNC](./Torno-CNC/README.md) y [Fresado-CNC](./Fresado-CNC/README.md). Aquí escribo el **proceso** de aprender, no el resultado.

> **Voz:** Primera persona, reflexiva. Los READMEs son para reclutadores; este archivo es para mí — y para cualquiera que quiera ver cómo se piensa al aprender CNC, no solo qué se aprendió.

---

## Cómo está organizado

Por **concepto técnico**, no por orden cronológico. Cuando vuelvo a buscar algo, lo busco por tema (*"¿cómo se calcula I/J?"*), no por fecha. Cada entrada tiene la misma estructura:

- **Qué entendí mal al inicio** — el malentendido específico.
- **Qué entiendo ahora** — el modelo mental correcto.
- **Cómo lo corregí** — la metodología que me funcionó.
- **Referencia** — qué archivo del repo materializa este aprendizaje.

---

## Índice de conceptos

1. [Interpolación circular: G02 vs G03](#1-interpolación-circular-g02-vs-g03)
2. [Método I/J para arcos](#2-método-ij-para-arcos)
3. [Coordenadas absolutas G90 vs incrementales G91](#3-coordenadas-absolutas-g90-vs-incrementales-g91)
4. [Ciclos fijos: por qué existen](#4-ciclos-fijos-por-qué-existen)
5. [G73 vs G83: cuándo cuál](#5-g73-vs-g83-cuándo-cuál)
6. [Velocidad de husillo y SFM](#6-velocidad-de-husillo-y-sfm)
7. [Comandos M comentados accidentalmente](#7-comandos-m-comentados-accidentalmente)
8. [Numeración de líneas: cómo no romper la secuencia](#8-numeración-de-líneas-cómo-no-romper-la-secuencia)
9. [Geometría desviada: el peligro de programar de memoria](#9-geometría-desviada-el-peligro-de-programar-de-memoria)
10. [Tabla rápida de errores recurrentes](#tabla-rápida-de-errores-recurrentes)

---

## 1. Interpolación circular: G02 vs G03

### Qué entendí mal al inicio

Pensaba que G02 y G03 eran "uno para arcos cóncavos y otro para convexos". Asocié la dirección del arco con su forma percibida en el plano.

### Qué entiendo ahora

G02 y G03 **no se refieren a la forma del arco**, se refieren a la **dirección de rotación de la herramienta vista desde el eje +Z**:

- **G02** = *clockwise* (sentido horario, como las manecillas del reloj).
- **G03** = *counter-clockwise* (sentido antihorario).

La forma del arco (cóncava o convexa) depende del observador y del punto de referencia. La dirección de rotación es **invariante**: la regla de la mano derecha siempre la decide.

### Cómo lo corregí

Antes de escribir cualquier G02/G03, dibujo el arco en papel y trazo la dirección con el dedo desde el inicio hacia el fin. Si va en sentido contrario a las manecillas del reloj **vista desde arriba (+Z)** → G03. Si va en sentido de las manecillas → G02.

Es lento al principio. Después de cinco arcos se vuelve automático.

### Referencia

`Fresado-CNC/ejercicios-letra-S/O0004_S_Absoluto_R.nc` — primer ejercicio donde tuve que decidir G02 vs G03 conscientemente.

---

## 2. Método I/J para arcos

Este fue **mi error técnico más significativo** hasta el momento. Lo documento con detalle porque la metodología que extraje sirve para cualquier arco futuro.

### Qué entendí mal al inicio

Asumí que I y J eran **el radio del arco** descompuesto en componentes. Si el arco tenía radio 1.5", supuse que I = 1.5 si el arco era horizontal o J = 1.5 si era vertical.

Mi código fue:
```gcode
N45 G03 X1.5 Y0 I1.5 J0
```

Esperaba un semicírculo de (0, 1.5) a (1.5, 0). Obtuve un arco de 90° en lugar de 180°.

### Qué entiendo ahora

I y J **no son el radio**. Son los **offsets desde el punto de inicio hasta el centro del arco**, en X y Y respectivamente.

El centro del arco es lo que importa. La máquina ya sabe el radio porque puede calcularlo desde la distancia inicio-centro. Lo que necesita es **dónde está el centro**.

Tres consecuencias importantes de esto:

1. I/J **siempre se miden desde el punto de inicio**, no desde el origen absoluto del programa.
2. I/J pueden ser **negativos** (centro a la izquierda o abajo del inicio).
3. El punto final solo sirve para **validar** — la máquina verifica que la distancia inicio-centro sea igual a la distancia fin-centro. Si no coinciden, el arco es geométricamente imposible y la máquina genera error.

### Cómo lo corregí — metodología que ahora aplico

**Paso 1: Encontrar el centro del arco.**

Si es semicírculo (180°), el centro está en el punto medio entre inicio y fin:
```
X_centro = (X_inicio + X_final) / 2
Y_centro = (Y_inicio + Y_final) / 2
```

Para arcos no-semicirculares, hay que usar geometría — pero la mayoría de mis ejercicios actuales son semicírculos.

**Paso 2: Calcular I y J como offsets.**
```
I = X_centro − X_inicio
J = Y_centro − Y_inicio
```

**Paso 3: Verificar signos por ubicación geométrica.**

- I positivo → centro a la **derecha** del inicio.
- I negativo → centro a la **izquierda** del inicio.
- J positivo → centro **arriba** del inicio.
- J negativo → centro **abajo** del inicio.

Si el resultado contradice mi intuición geométrica, el cálculo está mal.

**Paso 4: Aplicar al comando.**
```gcode
G02/G03 X_final Y_final I_calculado J_calculado
```

Aplicado al ejercicio que fallé:
- Inicio: (0, 1.5). Fin: (1.5, 0). Semicírculo.
- Centro: ((0+1.5)/2, (1.5+0)/2) = (0.75, 0.75).
- I = 0.75 − 0 = **0.75**.
- J = 0.75 − 1.5 = **−0.75**.

Código correcto:
```gcode
N45 G03 X1.5 Y0 I0.75 J-0.75
```

### Por qué la industria prefiere I/J sobre R

R puede ser ambiguo en arcos > 180° (un mismo R produce dos arcos posibles). I/J es siempre inequívoco porque el centro es único. Por eso los CAM industriales generan I/J por defecto.

### Referencia

`Fresado-CNC/ejercicios-letra-S/O0006_S_Absoluto_IJ_375.nc` — programa donde cometí el error y lo dejé documentado.

---

## 3. Coordenadas absolutas G90 vs incrementales G91

### Qué entendí mal al inicio

Pensaba que G91 era "más fácil" porque parecía intuitivo: *"avanza 5 mm a la derecha"* suena más natural que *"ve a la posición X=27.3"*.

### Qué entiendo ahora

G91 es más fácil **localmente** y más difícil **globalmente**.

- **Localmente**: cada bloque es intuitivo (avanza, sube, gira). Los patrones repetitivos se escriben más fácil.
- **Globalmente**: pierdo noción de dónde está la herramienta en coordenadas absolutas. Después de 20 líneas en G91, necesito calcular la posición absoluta sumando todos los movimientos previos. Si me equivoco en un cálculo intermedio, todo el resto del programa hereda el error.

### Cómo lo corregí

Adopté tres reglas personales:

1. **G90 por defecto** en todo programa. Solo cambio a G91 cuando hay simetría o repetición clara.
2. **Llevar tabla de posiciones** en papel mientras programo en G91, con tres columnas: línea, X absoluta, Y absoluta, movimiento incremental ejecutado.
3. **Volver a G90 periódicamente** en programas largos para "reanclarme" a coordenadas absolutas y evitar errores acumulados.

### Referencia

Comparar `O0004_S_Absoluto_R.nc` (todo G90) con `O0005_S_Incremental_G91_R.nc` (todo G91) muestra el contraste de ambos enfoques sobre la misma pieza.

---

## 4. Ciclos fijos: por qué existen

### Qué entendí mal al inicio

Pensaba que los ciclos fijos (G81, G83, etc.) eran "atajos opcionales" — que si escribía los movimientos manualmente con G00/G01, conseguía el mismo resultado.

Mi primera versión de taladrado de 10 agujeros tenía **40 líneas**: 4 movimientos por agujero (posicionar XY → bajar Z rápido → bajar Z corte → subir Z) × 10 agujeros.

### Qué entiendo ahora

Los ciclos fijos no son opcionales — son la forma profesionalmente correcta. Tres razones:

1. **Reducen errores de transcripción**: una sola línea define el patrón completo.
2. **Son legibles**: `G81 X20 Y15 Z-5 R1 F100` comunica intención (taladrar) además de movimiento.
3. **Son optimizados internamente**: el control aplica trayectorias eficientes que no replicaría con G00/G01 manual.

La versión con G81 reduce 40 líneas a:
```gcode
N30 G81 X20 Y15 Z-5 R1 F100
N35 X40
N40 X60
N45 X80
N50 X100
N55 G80
```

### Cómo lo corregí

Adopté la regla: **si una operación se repite 3+ veces, busco el ciclo fijo correspondiente antes de escribirlo manual**. Si no existe ciclo, considero subrutina (M98/M99) — que aún no aplico pero sé que es el siguiente nivel.

### Referencia

`Fresado-CNC/ejercicios-cilindros/O0002_Cilindros_v1.nc` — primer programa donde apliqué G81.

---

## 5. G73 vs G83: cuándo cuál

### Qué entendí mal al inicio

Asumí que G73 y G83 eran intercambiables y la diferencia era cosmética.

### Qué entiendo ahora

Ambos son ciclos de taladrado profundo con picoteo (*peck drilling*) — entran al material, retraen, vuelven a entrar más profundo, etc. La diferencia crítica está en **cuánto retraen** entre picoteos:

- **G73** (*high-speed peck*): retracción **parcial**. Pierde menos tiempo, pero la viruta puede acumularse en agujeros profundos.
- **G83** (*peck drilling estándar*): retracción **completa** hasta plano de seguridad. Garantiza evacuación de viruta, pero es más lento.

### Cómo lo corregí

Regla que apliqué después del incidente:

- **Aluminio + agujeros profundos** (>3× diámetro): G83. La viruta de aluminio es larga y tiende a aglomerarse.
- **Acero + agujeros poco profundos**: G73 puede ser válido.
- **Cuando dudo**: G83. La penalización en tiempo es menor que el costo de romper una broca por viruta atascada.

### Referencia

Comparar `O0002_Cilindros_v1.nc` (G73) con `O0003_Cilindros_v2.nc` (G83) — la versión 2 corrige el error de la 1.

---

## 6. Velocidad de husillo y SFM

### Qué entendí mal al inicio

Pensaba que las RPM eran un parámetro arbitrario que se elegía "razonablemente". Cuando cambié de fresa 1/2" a 3/8", mantuve el mismo RPM y el simulador no se quejó. Asumí que estaba bien.

### Qué entiendo ahora

RPM no es independiente — está determinado por el **SFM** (*Surface Feet per Minute*, velocidad de corte superficial), que sí es propiedad del material y la herramienta:

```
RPM = (SFM × 12) / (π × Diámetro_pulgadas)
```

Para aluminio con carburo, SFM ≈ 600–800. Eso significa:

- Fresa 1/2" → RPM ≈ 4500–6000.
- Fresa 3/8" → RPM ≈ 6000–8000.

**Herramientas más pequeñas necesitan MÁS RPM**, no menos. La razón física: el perímetro es menor, así que la herramienta debe girar más rápido para mantener la misma velocidad lineal en el filo.

### Cómo lo corregí

En contexto didáctico (Denford), uso RPM conservadores (2000–2400) por dos razones:

1. Reduce riesgo en caso de programa con error.
2. Permite observar la simulación con calma.

Pero **declaro explícitamente en comentarios** del código que son valores didácticos, no de producción:

```gcode
N20 M03 S2400 (RPM DIDACTICO - PRODUCCION ~6000)
```

Esto es importante para la honestidad técnica del código y evita que alguien copie/pegue mis valores en producción real.

### Referencia

`Fresado-CNC/ejercicios-letra-S/O0006_S_Absoluto_IJ_375.nc` — primer ejercicio donde cambié de fresa 1/2" a 3/8" y tuve que pensar el ajuste de RPM.

---

## 7. Comandos M comentados accidentalmente

### Qué entendí mal al inicio

Vi en algún recurso un código con paréntesis y asumí que eran "agrupamiento" o "claridad visual", como en matemáticas o programación de software.

Mi código tenía:
```gcode
N20 (M03 S2000)
```

Esperaba que el husillo arrancara. No arrancó. Tardé en entender por qué.

### Qué entiendo ahora

En G-code, los paréntesis convierten todo lo que está entre ellos en **comentario**. El controlador los ignora completamente. No son agrupamiento ni paréntesis matemáticos.

Es lo equivalente a `// comentario` en JavaScript o `# comentario` en Python.

### Cómo lo corregí

Regla mental: **"si quiero que la máquina lo ejecute, NUNCA va entre paréntesis"**. Los paréntesis son exclusivamente para metadata: nombre de operación, dimensiones del material, advertencias para el operador.

```gcode
(LETRA S - PROGRAMA DIDACTICO)        ← comentario informativo
N20 M03 S2000                          ← comando real, sin paréntesis
```

### Referencia

`Fresado-CNC/ejercicios-letra-S/O0004_S_Absoluto_R.nc` — preserva las primeras versiones donde cometí este error.

---

## 8. Numeración de líneas: cómo no romper la secuencia

### Qué entendí mal al inicio

Numeré líneas con incremento de 1: N1, N2, N3, N4...

Funcionaba hasta que tuve que **insertar** una línea entre N5 y N6. Renombré todo desde ahí hacia adelante. Llevó tiempo y generé líneas duplicadas accidentalmente:

```gcode
N125 G01 X0
N125 G01 Y0   ← Duplicado por error de renombrado
```

Algunos controladores ejecutan solo el primer N125 y silenciosamente ignoran el segundo. Otros tiran error. Ninguno te avisa "tienes duplicados".

### Qué entiendo ahora

La convención industrial estándar es **incrementar de 5 en 5 o de 10 en 10**: N10, N20, N30...

La razón es simple: deja **espacio para insertar** sin renumerar. Si necesito agregar algo entre N20 y N30, lo numero N25.

### Cómo lo corregí

Adopté incremento de 5. Es el balance entre:

- Demasiado pequeño (1) → no deja espacio para insertar.
- Demasiado grande (100) → desperdicia números, los archivos se ven raros.
- 5 o 10 → estándar de industria, balance óptimo.

### Referencia

Aplicado consistentemente desde `O0004` en adelante.

---

## 9. Geometría desviada: el peligro de programar de memoria

### Qué entendí mal al inicio

Después de mirar el plano por unos minutos, pensé que tenía las coordenadas memorizadas. Dejé el plano a un lado y programé "de cabeza".

Resultado: en `O0006`, programé el segundo arco de la letra S con destino (1.5, 3) cuando el plano decía (3, 1.5). Las coordenadas estaban transpuestas en mi memoria.

### Qué entiendo ahora

La memoria de trabajo humana es **limitada y poco confiable** para datos numéricos sin estructura. Confundir 1.5/3 con 3/1.5 es un error de tipo "transposición" que el cerebro comete sistemáticamente bajo carga cognitiva.

Los profesionales de CNC **siempre tienen el plano físicamente a la vista durante la programación**. No es opcional ni señal de novicio — es protocolo.

### Cómo lo corregí

Tres cambios de hábito:

1. **Plano impreso o en pantalla, siempre visible**, durante toda la programación.
2. **Verificar coordenada por coordenada** contra el plano antes de pasar a la siguiente línea.
3. **Cuando un movimiento parezca "raro" en simulación, verificar contra plano antes de tocar el código**. La intuición de que algo está mal suele ser correcta — lo que está mal es la coordenada, no la simulación.

### Referencia

`Fresado-CNC/ejercicios-letra-S/O0006_S_Absoluto_IJ_375.nc` — preserva el error original como evidencia.

---

## Tabla rápida de errores recurrentes

Para consulta veloz cuando reviso código antes de simular:

| # | Error | Síntoma | Corrección |
|---|---|---|---|
| 1 | I/J como radio | Arco de 90° donde esperaba 180° | Calcular centro, restar inicio |
| 2 | M comentado entre paréntesis | Husillo no arranca, refrigerante no abre | Quitar paréntesis del comando |
| 3 | Líneas duplicadas (N125 × 2) | Comportamiento errático en máquina | Renumerar con incremento de 5 |
| 4 | G01 sin coordenadas | Error de ejecución o nada se mueve | Verificar X/Y/Z explícitos |
| 5 | G02/G03 invertidos | Arco va en dirección contraria | Regla de mano derecha desde +Z |
| 6 | Pierdo posición en G91 | No sé dónde está la herramienta | Volver a G90 periódicamente |
| 7 | Sin retracción Z antes de M30 | Posible colisión al cambiar pieza | Checklist: Z safe → M05 → M30 |
| 8 | Coordenadas transpuestas (X/Y intercambiadas) | Geometría desviada | Plano siempre visible, verificar |
| 9 | RPM iguales para herramienta de distinto diámetro | Acabado pobre, desgaste excesivo | Recalcular con SFM al cambiar herramienta |
| 10 | Parchar arco erróneo con G01 lineales | Pieza con muescas raras | Corregir el arco, no compensar con líneas |

---

## Patrones que noto en mí mismo

Reflexiones sobre **cómo** aprendo, no qué aprendo. Esta sección la actualizo cuando reconozco un patrón nuevo.

### Tiendo a saltar la simulación cuando creo que el código está "obviamente bien"

He cometido el mismo tipo de error tres veces: termino un programa, tengo confianza en él, ejecuto sin simular completamente, y descubro un error que la simulación habría detectado en 30 segundos. La lección no es "ten más cuidado" — es **forzarme a simular siempre**, sin excepciones, incluso cuando creo que es innecesario.

La regla que adopté: **un programa no está terminado hasta que pasa simulación completa, paso a paso, en single block**.

### Confundo "comprender un concepto" con "saber aplicarlo"

Leí sobre I/J en un manual antes de programar O0006. Cuando llegué a programar, asumí que entender la teoría equivalía a poder aplicarla. No es lo mismo. Comprender es pasivo; aplicar requiere haber traducido el concepto a una metodología paso a paso.

La regla que adopté: **antes de aplicar un concepto nuevo, escribir la metodología en pasos numerados** (como hice arriba para I/J). Si no puedo escribir los pasos, no comprendí lo suficiente para aplicar.

### Error productivo es mejor que código perfecto desde el inicio

Mi versión inicial de cada ejercicio tiene errores. La segunda versión los corrige. La tercera optimiza. Este patrón no es señal de incompetencia — es **iteración**, que es como funciona la ingeniería real. El intento de "código perfecto al primer intento" lleva a parálisis.

---

## Siguiente entrada esperada

Cuando introduzca **compensación de radio (G41/G42)** en algún ejercicio futuro, vendrá una nueva sección. Ya sé conceptualmente qué hace (compensa por el radio de la herramienta para que la trayectoria programada coincida con el borde de la pieza), pero no la he aplicado. Cuando lo haga, lo más interesante será documentar **qué entendí mal al primer intento** — eso es lo que vale registrar.

---

**Última actualización:** Marzo 2026
**Estado:** Documento vivo, se nutre con cada concepto nuevo que cometo el error de no entender bien al inicio.