# 📚 LEARNING.md — Bitácora de Aprendizaje CNC

**Estudiante:** Benjamín  
**Institución:** CECATI No. 17  
**Período:** Enero - Febrero 2026  
**Enfoque:** Programación CNC con Denford FANUC Milling v1.96

---

## 🎯 Propósito de este Documento

Esta bitácora documenta mi viaje de aprendizaje en programación CNC, incluyendo:
- ✅ Conceptos aprendidos y dominados
- ❌ Errores cometidos y por qué ocurrieron
- 🔧 Soluciones aplicadas y lecciones extraídas
- 📈 Evolución desde código didáctico hacia mejores prácticas profesionales

> **Filosofía de aprendizaje:** Los ejercicios en `2.CNC/` son **didácticos e iterativos**. Priorizo comprender fundamentos (comandos, sintaxis, lógica de movimientos) antes que implementar código perfecto. Los errores documentados aquí son **parte esencial del proceso** de aprender haciendo.

---

## 📖 Índice

1. [Fase 1: Primeros Pasos con G-code](#fase-1-primeros-pasos-con-g-code)
2. [Fase 2: Interpolación Circular - Método R](#fase-2-interpolación-circular---método-r)
3. [Fase 3: Coordenadas Incrementales G91](#fase-3-coordenadas-incrementales-g91)
4. [Fase 4: Método I,J - El Desafío](#fase-4-método-ij---el-desafío)
5. [Errores Comunes y Soluciones](#errores-comunes-y-soluciones)
6. [Conceptos Fundamentales Aprendidos](#conceptos-fundamentales-aprendidos)
7. [Transición hacia Mejores Prácticas](#transición-hacia-mejores-prácticas)
8. [Próximos Pasos en mi Formación](#próximos-pasos-en-mi-formación)

---

## Fase 1: Primeros Pasos con G-code

### Ejercicio: Matriz de Cilindros (O0002, O0003)

#### 🎯 Objetivo
Crear un patrón de 10 cilindros (matriz 5×2) usando múltiples herramientas y ciclos fijos.

#### 📝 Conceptos Nuevos
- **Cambio de herramienta** con `M06 T##`
- **Ciclos fijos** de taladrado (G81, G73/G83)
- **Comandos Denford** específicos (G170/G171) para pocket milling
- Gestión de **múltiples operaciones** en un solo programa

#### ✅ Lo que Funcionó
```gcode
(BROCA DE CENTROS)
N20 M06 T01
N25 M03 S2000
N30 G00 X20 Y15
N35 G00 Z1
N40 G01 Z-5 F100        ← Centrado manual, simple
N45 G00 Z1              ← Retracción
```

**Por qué funcionó:** Secuencia clara y directa. Usar G01 para centrado es didáctico y permite ver el movimiento paso a paso.

#### ❌ Error Encontrado: Ciclo G81 vs Movimientos Manuales
**Mi código inicial:**
```gcode
N30 G00 X20 Y15
N35 G00 Z1
N40 G01 Z-5 F100
N45 G00 Z1
N50 G00 X40            ← Repetir todo el bloque para cada agujero
N55 G01 Z-5
N60 G00 Z1
```

**Problema:** Código repetitivo y largo. 10 agujeros = 40 líneas.

**Solución Aprendida:** Usar ciclo G81
```gcode
N30 G81 X20 Y15 Z-5 R1 F100    ← Primera posición + parámetros
N35 X40                         ← Solo coordenadas, repite ciclo
N40 X60
N45 X80
N50 X100
N55 G80                         ← Cancelar ciclo
```

**Lección:** Los ciclos fijos existen para eliminar repetición. Aprenderlos ahorra líneas y hace el código más legible.

#### 🔧 Mejora Aplicada: De G73 a G83

**Primera versión (O0002):**
```gcode
N187 G91 G73 X20 Z-22 R2 Q5 K5 F80
```

**Problema:** G73 no retrae completamente entre picoteos, viruta puede acumularse en agujeros profundos.

**Versión mejorada (O0003):**
```gcode
N187 G91 G83 X20 Z-22 R2 Q5 F80    ← G83 con retracción completa
```

**Lección:** G83 es más seguro para taladrado profundo en aluminio. Toma más tiempo pero garantiza evacuación de viruta.

#### 💡 Insight Clave
> **G170/G171 (Denford específico)** son comandos poderosos pero complejos. Mi primer intento tenía parámetros incorrectos. Aprendí que G170 *define* la geometría y G171 *ejecuta* el fresado. Son dos pasos separados, no un solo comando.

---

## Fase 2: Interpolación Circular - Método R

### Ejercicio: Letra S - Versión Absoluta (O0004)

#### 🎯 Objetivo
Trazar contorno de letra "S" usando arcos circulares (G02/G03) con el método del radio (R).

#### 📝 Conceptos Nuevos
- **G02** (arco horario) vs **G03** (arco antihorario)
- **Método R** para definir arcos: `G03 X1.5 Y0 R1.5`
- Diferencia entre arcos **cóncavos** (G02) y **convexos** (G03)
- Secuencia lógica de semicírculos para formar la "S"

#### ✅ Mi Primer Arco Exitoso
```gcode
N55 G03 X1.5 Y0 R1.5
```
**Inicio:** (0, 1.5)  
**Fin:** (1.5, 0)  
**Radio:** 1.5"  
**Resultado:** Semicírculo perfecto de 180°

**Por qué funcionó:** 
- Radio R es simple e intuitivo
- Para semicírculos el cálculo es directo: R = distancia entre inicio y fin / 2 (en línea recta sería 2.12", pero el arco necesita R=1.5" para cubrir 180°)

#### ❌ Error: Confusión entre G02 y G03

**Mi código inicial (línea N70):**
```gcode
N70 G02 X1 Y3.5 R.75        ← Arco pequeño de transición
```

**Problema:** En simulación el arco iba en dirección contraria a lo esperado.

**Causa raíz:** No visualicé correctamente la **regla de la mano derecha**:
- G02 (CW/horario) = pulgar apunta -Z, dedos indican rotación
- G03 (CCW/antihorario) = pulgar apunta +Z, dedos indican rotación

**Solución:** Cambié a G03 después de simular y verificar dirección.

**Lección:** 
> Antes de escribir G02/G03, dibujar el arco en papel y trazar la dirección con el dedo. Si va contra las manecillas del reloj visto desde arriba = G03.

#### ⚠️ Error Encontrado: Líneas Duplicadas N125

```gcode
N125 G01 X0
N125 G01 Y0        ← ERROR: Mismo número de línea
```

**Problema:** Algunas máquinas rechazan esto o solo ejecutan la primera línea.

**Causa:** Copiar/pegar sin actualizar numeración.

**Solución:** Numerar secuencialmente:
```gcode
N125 G01 X0
N130 G01 Y0
```

**Lección:** Usar incrementos de 5 o 10 (N10, N20, N30...) permite insertar líneas después sin renumerar todo.

#### ❌ Error: Comando Incompleto

```gcode
N145 G01           ← Sin coordenadas X, Y, o Z
```

**Problema:** G01 requiere al menos una coordenada de destino.

**Causa:** Borré las coordenadas durante edición y no me di cuenta.

**Solución:** Siempre verificar que cada G01 tenga destino.

**Lección:** Simular SIEMPRE antes de dar por terminado un programa. El simulador detecta estos errores inmediatamente.

---

## Fase 3: Coordenadas Incrementales G91

### Ejercicio: Letra S - Versión Incremental (O0005)

#### 🎯 Objetivo
Reescribir O0004 usando **coordenadas incrementales** (G91) en lugar de absolutas (G90).

#### 📝 Conceptos Nuevos
- **G91:** Todas las coordenadas son relativas a la posición actual
- Conversión mental: "moverme +X desde donde estoy" vs "ir a posición X absoluta"
- Ventaja: Patrones repetitivos son más fáciles de escribir

#### ✅ Lo que Aprendí: Conversión Absoluto → Incremental

**Código absoluto (G90):**
```gcode
N50 G01 X0          ← Posición actual: (-0.5, 1.5)
N55 G03 X1.5 Y0 R1.5   ← Ir a (1.5, 0) absoluto
```

**Código incremental (G91):**
```gcode
N30 G01 X0          ← Me muevo de -0.5 a 0 = +0.5 en X
N35 G91             ← Activo modo incremental
N40 G03 X1.5 Y-1.5 R1.5   ← Desde (0, 1.5), moverme +1.5 en X, -1.5 en Y
```

**Fórmula de conversión:**
```
X_incremental = X_destino - X_actual
Y_incremental = Y_destino - Y_actual
```

#### 💡 Ventaja Descubierta: Patrones Repetitivos

En O0005, las transiciones pequeñas fueron más fáciles:
```gcode
N55 G02 X-.5 Y.5 R.75
N60 G02 X.5 Y.5          ← Reusar mismo movimiento relativo
N65 G02 X.5 Y-.5         ← Solo cambio de signo
```

**Lección:** G91 brilla cuando hay **simetría** o **repeticiones** en el diseño.

#### ⚠️ Problema Encontrado: Perder Noción de Posición Absoluta

Después de 20 líneas en G91, **no sabía dónde estaba la herramienta** en coordenadas absolutas.

**Solución adoptada:** Llevar tabla mental o en papel:
```
Línea | X_abs | Y_abs | Movimiento incremental
------|-------|-------|----------------------
N40   |  1.5  |  0    | X+1.5 Y-1.5
N45   |  3.0  |  1.5  | X+1.5 Y+1.5
N50   |  1.5  |  3.0  | X-1.5 Y+1.5
```

**Lección:** 
> G91 es poderoso pero requiere **disciplina** para rastrear posición. En programas largos, considerar regresar a G90 periódicamente para verificar posición absoluta.

---

## Fase 4: Método I,J - El Desafío

### Ejercicio: Letra S con I,J (O0006)

#### 🎯 Objetivo
Usar el método **I,J** (offset al centro del arco) en lugar de R para ganar precisión.

#### 📝 Conceptos Nuevos
- **I** = Distancia en X desde **punto de inicio** (no origen) hasta el centro del arco
- **J** = Distancia en Y desde **punto de inicio** hasta el centro del arco
- Siempre incremental desde el punto actual, nunca desde (0,0)
- Método estándar en industria y software CAM

#### ❌ **ERROR CRÍTICO: Confusión entre Radio e I,J**

**Mi código (línea N45):**
```gcode
N45 G03 X1.5 Y0 I1.5 J0
```

**¿Qué esperaba?**  
Un semicírculo de (0, 1.5) a (1.5, 0) con radio 1.5"

**¿Qué obtuve?**  
Un arco de 90° (cuarto de círculo) en lugar de 180°

**Diagnóstico del error:**
```
Inicio:  (0, 1.5)
Destino: (1.5, 0)

Mi I,J:  I=1.5, J=0
Centro calculado por la máquina: (0+1.5, 1.5+0) = (1.5, 1.5)

Centro CORRECTO para semicírculo: (0.75, 0.75)

Por lo tanto:
I correcto = 0.75 - 0 = 0.75
J correcto = 0.75 - 1.5 = -0.75
```

**Causa raíz:** Usé el **radio** (1.5) como valor de I, pensando que I era una "distancia total". No entendí que I,J son **offsets incrementales** desde el inicio.

#### 🔧 Cómo Corregir el Error

**Paso 1:** Encontrar el centro del arco
Para un semicírculo, el centro está en el **punto medio**:
```
X_centro = (X_inicio + X_final) / 2 = (0 + 1.5) / 2 = 0.75
Y_centro = (Y_inicio + Y_final) / 2 = (1.5 + 0) / 2 = 0.75
```

**Paso 2:** Calcular I,J desde el inicio
```
I = X_centro - X_inicio = 0.75 - 0 = 0.75
J = Y_centro - Y_inicio = 0.75 - 1.5 = -0.75
```

**Código correcto:**
```gcode
N45 G03 X1.5 Y0 I0.75 J-0.75
```

#### 📐 Metodología de Cálculo I,J (lo que aprendí)

**Para CUALQUIER arco:**

1. **Identificar puntos:**
   - Inicio: donde está la herramienta AHORA
   - Fin: donde quiero llegar
   - Radio del arco (del diseño)

2. **Encontrar el centro:**
   - Si es semicírculo (180°): centro = punto medio
   - Si es arco menor: usar geometría (triángulos, Pitágoras)
   - Si es arco mayor (>180°): método avanzado

3. **Calcular I,J:**
   ```
   I = X_centro - X_inicio
   J = Y_centro - Y_inicio
   ```

4. **Verificar signos:**
   - I positivo → centro a la DERECHA del inicio
   - I negativo → centro a la IZQUIERDA
   - J positivo → centro ARRIBA del inicio
   - J negativo → centro ABAJO

5. **Escribir comando:**
   ```gcode
   G02/G03 X_final Y_final I_calculado J_calculado
   ```

#### 💡 Insight Clave sobre I,J

> **El valor de I,J NO depende del punto final.**  
> Solo dependen de dónde está el inicio y dónde está el centro.  
> La máquina usa el punto final para **validar** que el arco sea posible (distancia inicio-centro = distancia fin-centro).

#### ⚠️ Otros Errores en O0006

**Error 2: Geometría Desviada (línea N50)**
```gcode
N50 G03 X1.5 Y3 I0 J1.5
```

**Problema:** El segundo arco debería ir de (1.5, 0) a (3, 1.5), pero programé (1.5, 3).

**Causa:** No seguí el diseño original, inventé coordenadas.

**Lección:** Siempre tener el **plano técnico** a la vista durante programación. No confiar en memoria.

**Error 3: Movimientos de Ajuste Manual**
```gcode
N65 G01 X1.5 Y3.7
N70 G01 X1.2 Y3.4
N75 G01 X2 Y3.4
N80 G01 Y3.3
```

**Problema:** Estos movimientos no están en el diseño. Los agregué para "arreglar" errores de arcos anteriores.

**Causa raíz:** En lugar de corregir los I,J incorrectos, intenté compensar con movimientos lineales adicionales.

**Lección:** 
> Nunca "parchear" errores con movimientos extra. Si el arco está mal, **corregir el arco**. El código limpio es código correcto desde el inicio.

---

## Fase 5: Aprendizaje de Velocidades y RPM

### Ejercicio: Cambio de Herramienta de 1/2" a 3/8"

#### 🎯 Objetivo
Entender la relación entre **diámetro de herramienta** y **RPM** necesario.

#### 📝 Concepto Aprendido: SFM (Surface Feet per Minute)

**Fórmula:**
```
RPM = (SFM × 12) / (π × Diámetro_pulgadas)
```

**Para aluminio con fresa de carburo:**
- SFM típico = 600-800 (usaremos 600 para ser conservadores)

**Herramienta 1/2" (0.5"):**
```
RPM = (600 × 12) / (π × 0.5)
RPM = 7200 / 1.57
RPM ≈ 4580

En ejercicio didáctico usé: 2000 RPM (conservador para aprendizaje)
```

**Herramienta 3/8" (0.375"):**
```
RPM = (600 × 12) / (π × 0.375)
RPM = 7200 / 1.178
RPM ≈ 6112

En ejercicio didáctico usé: 2400 RPM
```

**Proporción:**
```
RPM_3/8 / RPM_1/2 = 2400 / 2000 = 1.2 (20% más rápido)
```

#### 💡 Regla Práctica Aprendida
> **Herramientas más pequeñas → RPM más altos**  
> El perímetro es menor, entonces deben girar más rápido para mantener la misma velocidad de superficie (SFM).

#### ⚠️ Nota sobre Valores Didácticos

Los RPM que usé (2000-2400) son **muy conservadores** comparados con lo óptimo (4500-6100). Esto es **intencional** en fase de aprendizaje:

**Ventajas de RPM conservadores:**
- ✅ Menos riesgo de rotura de herramienta
- ✅ Más tiempo para observar la simulación
- ✅ Menor carga en el husillo del simulador

**Desventaja:**
- ⚠️ Tiempos de ciclo más largos (no importa en simulación)

**Lección:**  
> En producción real, calcular RPM óptimos por material y herramienta es crítico para eficiencia. En aprendizaje, ser conservador es seguro.

---

## Errores Comunes y Soluciones

### 📋 Tabla de Errores Frecuentes

| # | Error | Causa | Solución | Lección |
|---|-------|-------|----------|---------|
| 1 | **I,J = Radio** | No entender que I,J son offsets desde inicio | Calcular centro, luego I = X_c - X_i, J = Y_c - Y_i | I,J siempre desde punto actual |
| 2 | **Comandos M comentados** `(M03 S2000` | Paréntesis convierten en comentario | Quitar paréntesis: `M03 S2000` | Paréntesis = comentarios, no código |
| 3 | **Líneas duplicadas** (N125 × 2) | Copiar sin actualizar número | Numerar secuencialmente con incrementos de 5-10 | Usar N10, N20, N30... permite insertar |
| 4 | **G01 sin coordenadas** | Borrado accidental durante edición | Verificar que cada G01 tenga X, Y, o Z | Simular siempre antes de dar por hecho |
| 5 | **Confusión G02/G03** | No visualizar dirección del arco | Dibujar en papel, aplicar regla mano derecha | G03 = contra reloj visto desde +Z |
| 6 | **Arcos de 180° con R** | R puede ser ambiguo en semicírculos | Usar signo: R+ para arco menor, R- para mayor | Mejor usar I,J para arcos de 180° |
| 7 | **Perder posición en G91** | Modo incremental sin rastreo | Llevar tabla de posiciones acumuladas | Volver a G90 periódicamente |
| 8 | **Sin retracción final** | Olvidar G00 Z1.0 antes de M30 | Siempre: Z segura → M05 → M30 | Checklist de finalización |
| 9 | **Punto decimal incorrecto** `X10.0` vs `X10` | Inconsistencia en notación | FANUC acepta ambas, pero ser consistente | Preferir `.0` para claridad |
| 10 | **Geometría desviada** | No seguir plano técnico | Tener dibujo a la vista, verificar cada coord | Medir dos veces, programar una |

---

## Conceptos Fundamentales Aprendidos

### 1. Interpolación Circular (G02/G03)

**Dominado:**
- ✅ Diferencia entre G02 (CW) y G03 (CCW)
- ✅ Método R para arcos simples
- ✅ Visualizar dirección de arcos en papel

**En progreso:**
- 🔄 Método I,J (conceptualmente entendido, requiere más práctica)
- 🔄 Arcos complejos (>180° o <180°)

### 2. Sistemas de Coordenadas

**Dominado:**
- ✅ G90 (absoluto) para programación clara
- ✅ G91 (incremental) para patrones repetitivos
- ✅ Conversión entre absoluto e incremental

**Pendiente:**
- ⏳ G54-G59 (offsets de trabajo múltiples)
- ⏳ G92 (shift de origen temporal)

### 3. Ciclos Fijos

**Dominado:**
- ✅ G81 (taladrado simple)
- ✅ G73/G83 (taladrado profundo con picoteo)
- ✅ G80 (cancelar ciclo)

**Pendiente:**
- ⏳ G82 (taladrado con pausa)
- ⏳ G84 (roscado)
- ⏳ G85-G89 (mandrinado, escariado)

### 4. Gestión de Herramientas

**Dominado:**
- ✅ M06 T## (cambio de herramienta)
- ✅ Relación diámetro ↔ RPM
- ✅ Uso de múltiples herramientas en un programa

**Pendiente:**
- ⏳ Compensación de radio (G41/G42)
- ⏳ Compensación de longitud (G43/G44)
- ⏳ Offsets de herramienta (D##, H##)

### 5. Estructura de Programa

**Dominado:**
- ✅ Secuencia básica: Setup → Posicionamiento → Corte → Retorno
- ✅ Uso de comentarios `( )`
- ✅ Numeración de líneas N##

**Pendiente:**
- ⏳ Inicialización completa (G21 G17 G40 G49 G80 G90)
- ⏳ Subrutinas (M98/M99)
- ⏳ Variables y macros (#####)

---

## Transición hacia Mejores Prácticas

### 📊 Comparación: Mi Código Actual vs Profesional

#### Mi Código Didáctico (O0004)
```gcode
O0004
(CORTADORA .5)
N20 G20 G80 G54 G90
N25 G28 G40 G95
N30 M06 T01
N35 G00 X-.5 Y1.5
N40 G00 Z.1
N45 G01 Z-.250 F100
N50 G01 X0
N55 G03 X1.5 Y0 R1.5
[...]
N155 M30 M05
```

**Características:**
- ✅ Funciona en simulador
- ✅ Geometría básica correcta
- ⚠️ Comandos M incompletos
- ⚠️ Una sola pasada profunda
- ⚠️ Sin retracción segura

#### Código Profesional (Objetivo)
```gcode
%
O0004 (LETRA S - PRODUCCION)
(PROGRAMADOR: BENJAMIN - CECATI 17)
(FECHA: 2026-02-17)
(MATERIAL: ALUMINIO 6061 - 3" X 5" X 0.75")
(HERRAMIENTA: T01 - FRESA PLANA 1/2" CARBURO)

(SECCION: INICIALIZACION)
N10 G21 G17 G40 G49 G80 G90   (Reset completo)
N15 G20                        (Pulgadas)
N20 G54                        (Offset trabajo 1)
N25 G28 G91 Z0                 (Home Z)
N30 G90                        (Volver a absoluto)

(SECCION: SETUP HERRAMIENTA)
N35 T01 M06                    (Cambio a T01)
N40 S2000 M03                  (Husillo ON 2000 RPM)
N45 G43 H01 Z1.0               (Comp. longitud + altura segura)
N50 M08                        (Refrigerante ON)

(SECCION: POSICIONAMIENTO)
N55 G00 X-0.5 Y1.5             (Posición inicial)
N60 G00 Z0.1                   (Aproximación)

(SECCION: CORTE - PASADA 1 DE 2)
N65 G01 Z-0.125 F10.0          (Penetra 50% profundidad)
N70 G01 X0 F50.0               (Inicia contorno)
N75 G03 X1.5 Y0 R1.5
N80 G03 X3 Y1.5 R1.5
[... contorno completo ...]
N145 G01 X-0.5 Y1.5            (Retorno a inicio)

(SECCION: CORTE - PASADA 2 DE 2)
N150 G01 Z-0.125 F10.0         (Profundidad final)
N155 G01 X0 F50.0
[... contorno de nuevo ...]
N220 G01 X-0.5 Y1.5

(SECCION: FINALIZACION)
N225 G00 Z1.0                  (Retracción segura)
N230 M09                       (Refrigerante OFF)
N235 M05                       (Husillo OFF)
N240 G91 G28 Z0                (Home Z)
N245 G28 X0 Y0                 (Home XY)
N250 G90                       (Absoluto)
N255 M30                       (Fin programa)
%
```

**Diferencias clave:**
- ✅ Header con metadata (programador, fecha, material, herramienta)
- ✅ Reset completo de máquina (G21 G17 G40 G49 G80)
- ✅ Compensación de longitud (G43 H01)
- ✅ Refrigerante activo (M08/M09)
- ✅ **Dos pasadas** incrementales (-0.125" cada una)
- ✅ Velocidades diferenciadas (F10 penetración, F50 contorno)
- ✅ Retracción completa y home al final
- ✅ Secciones comentadas para claridad

### 📈 Plan de Progresión

#### ✅ Fase 1: Fundamentos (COMPLETADA)
- [x] Comandos G00, G01, G02, G03
- [x] Modo G90 vs G91
- [x] Ciclos fijos básicos
- [x] Cambio de herramienta
- [x] Método R para arcos

#### 🔄 Fase 2: Refinamiento (EN PROGRESO)
- [x] Método I,J conceptualmente
- [ ] I,J en práctica (3+ ejercicios más)
- [ ] Múltiples pasadas (DOC incremental)
- [ ] Velocidades diferenciadas por operación
- [ ] Headers y comentarios detallados

#### ⏳ Fase 3: Técnicas Avanzadas (PRÓXIMAMENTE)
- [ ] Compensación de radio G41/G42
- [ ] Subrutinas M98/M99
- [ ] Estrategias de desbaste vs acabado
- [ ] Optimización de trayectorias
- [ ] Introducción a CAM (generar código desde SolidWorks)

#### ⏳ Fase 4: Profesionalización (OBJETIVO)
- [ ] Código listo para producción
- [ ] Documentación técnica completa
- [ ] Optimización de tiempos de ciclo
- [ ] Control de calidad dimensional
- [ ] Mantenimiento preventivo de herramientas

---

## Próximos Pasos en mi Formación

### 🎯 Objetivos Inmediatos (Próximas 2 Semanas)

1. **Dominar cálculo de I,J**
   - Realizar 5 ejercicios adicionales con arcos diferentes
   - Crear hoja de cálculo para verificar I,J manualmente
   - Practicar arcos menores a 90° y mayores a 180°

2. **Implementar múltiples pasadas**
   - Reescribir O0004 con 2 pasadas de 0.125" cada una
   - Comparar tiempos de simulación vs pasada única
   - Documentar ventajas (vida herramienta, acabado)

3. **Estudiar compensación G41/G42**
   - Leer manual de Denford sobre compensación
   - Entender diferencia entre trayectoria programada vs real
   - Ejercicio simple: cuadrado con compensación

### 🎯 Objetivos a Mediano Plazo (Próximos 2 Meses)

4. **Introducción a CAM**
   - Diseñar pieza simple en SolidWorks
   - Usar SolidWorks CAM para generar trayectorias
   - Comparar código generado vs mi código manual
   - Identificar patrones profesionales

5. **Proyecto Integrador**
   - Diseñar pieza original (no ejercicio del profesor)
   - Programar con todas las mejores prácticas aprendidas
   - Simular y corregir errores
   - Documentar completamente

### 📚 Recursos de Estudio Próximos

- [ ] Manual completo de Fanuc (referencia oficial)
- [ ] Curso online de programación CAM
- [ ] Libros recomendados por el profesor
- [ ] Videos de operadores profesionales en YouTube

---

## 💡 Reflexiones Finales

### Lo Más Importante que Aprendí

> **Los errores son valiosos.** Cada error en mi código (I,J incorrectos, comandos M comentados, líneas duplicadas) me enseñó más que cuando algo funcionó a la primera. Documentar estos errores en `LEARNING.md` solidifica el aprendizaje y me permite evitarlos en el futuro.

### Cambio de Mentalidad

**Antes:**  
"Quiero que mi código funcione sin errores en el primer intento"

**Ahora:**  
"Voy a iterar, cometer errores, simular, corregir, y documentar el proceso. El código perfecto es el resultado de múltiples refinamientos."

### Agradecimientos

- **Profesor de CECATI 17:** Por ejercicios estructurados y feedback directo
- **Claude (Anthropic AI):** Por análisis detallados, identificación de errores, y guías paso a paso
- **Comunidad de programadores CNC:** Por cheatsheets y recursos compartidos

---

**Última actualización:** 17 de Febrero 2026  
**Siguiente revisión:** Después de completar 5 ejercicios más con método I,J

---

## 📎 Apéndice: Recursos y Referencias

### Cheatsheets en mi Carpeta `/recursos`
- `Cheatsheet_CNC_Torno_Fresa.png` — Comandos G/M por categoría
- `Cheatsheet_Denford_Fanuc_v1.png` — Tabla de comandos Denford
- `G_code_Fanuc.html` — Guía interactiva HTML

### Enlaces Útiles (Externos)
- Manual Denford: [Sitio oficial](https://www.denford.co.uk)
- Fanuc G-code reference: Búsqueda "Fanuc G-code quick reference PDF"
- Foros de CNC: CNCzone, Practical Machinist

### Próximos Documentos a Crear
- [ ] `CHEATSHEET_IJ_METHOD.md` — Guía rápida de cálculo I,J con ejemplos
- [ ] `BEST_PRACTICES.md` — Checklist de código profesional
- [ ] `PROJECT_LOG.md` — Bitácora de mi proyecto integrador final

---

*Este documento es un trabajo vivo. Se actualiza continuamente a medida que avanzo en mi formación.*
