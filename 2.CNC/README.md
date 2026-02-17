# 📁 2.CNC — Programación CNC | CECATI 17

Ejercicios de programación G-code en el simulador **Denford FANUC Milling v1.96**.  
Todos los programas están probados en simulación 2D y 3D dentro del software.

> ⚠️ **NOTA DIDÁCTICA:** Los programas en este directorio son ejercicios de aprendizaje enfocados en comprender comandos G-code, modos de coordenadas y métodos de interpolación. **No implementan todas las mejores prácticas industriales** (múltiples pasadas, optimización de velocidades, seguridad completa) ya que el objetivo es dominar fundamentos antes de aplicar técnicas avanzadas. El progreso hacia código profesional se documenta en `LEARNING.md`.

---

## 🗂️ Estructura de esta carpeta

```
2.CNC/
├── ejercicios-cilindros/
│   ├── planos/
│   │   ├── 1.0(Enero).png
│   │   ├── 2.0(Enero).png
│   │   └── 3.0(Febrero).png
│   ├── simulaciones/
│   │   ├── O0002_Cilindros_v1_simulacion_2D.png
│   │   ├── O0002_Cilindros_v1_simulacion_3D.png
│   │   ├── O0003_Cilindros_v2_simulacion_2D.png
│   │   └── O0003_Cilindros_v2_simulacion_3D.png
│   ├── O0002_Cilindros_v1.nc
│   └── O0003_Cilindros_v2.nc
├── ejercicios-letra-S/
│   ├── planos/
│   │   └── (planos del profesor)
│   ├── simulaciones/
│   │   ├── FRESA4_simulacion_2D.png
│   │   ├── FRESA4_simulacion_3D.png
│   │   ├── FRESA5_simulacion_2D.png
│   │   ├── FRESA5_simulacion_3D.png
│   │   ├── FRESA6_simulacion_2D.png
│   │   ├── FRESA6_simulacion_3D.png
│   │   ├── FRESA7_simulacion_2D.png
│   │   └── FRESA7_simulacion_3D.png
│   ├── referencia/
│   │   ├── LetraS_resultado_mecanizado.png
│   │   └── LetraS_render_IA_adicional.png
│   ├── O0004_S_Absoluto_R.nc
│   ├── O0005_S_Incremental_G91_R.nc
│   ├── O0006_S_Absoluto_IJ_375.nc
│   └── O0007_S_Incremental_IJ_375.nc
├── planos/
│   └── Fotos_planos/
│       ├── 1.0 (Enero).png
│       ├── 2.0 (Enero).png
│       └── 3.0 (febrero).png
├── recursos/
│   ├── Manual/
│   │   └── (9 imágenes JPEG del manual del profesor)
│   ├── Cheatsheet_CNC_Torno_Fresa.png
│   ├── Cheatsheet_Denford_Fanuc_v1.png
│   ├── Cheatsheet_Denford_Fanuc_v2.png
│   ├── Cheatsheet_Denford_Fanuc.docx
│   ├── Cheatsheet_Programacion_CNC.png
│   ├── G_code_Fanuc.html
│   ├── Guia_Referencia_CNC.pdf
│   └── Guía_Rápida_Código_G.pdf
├── simulador-denforf-fanuc/
│   └── (vacío - espacio para archivos del simulador)
└── README.md  ← este archivo
```

---

## 🔩 Ejercicios Completados

### Serie 1: Matriz de Cilindros (Enero-Febrero 2026)

> **Material:** Aluminio 120×80×25mm · **Patrón:** 5×2 cilindros · **Multi-herramienta**

| # | Archivo | Herramientas | Operaciones | Descripción |
|---|---------|--------------|-------------|-------------|
| 1 | `O0002_Cilindros_v1.nc` | T01: Broca centros Ø5mm<br>T02: Broca Ø10mm<br>T03: Cortadora Ø9.5mm | Centrado (G81)<br>Perforado profundo (G73/G83)<br>Fresado de cilindros (G170/G171) | Primera versión del ejercicio de matriz 5×2. Introduce ciclos fijos de taladrado y comandos Denford G170/G171 para pocketing. |
| 2 | `O0003_Cilindros_v2.nc` | (Mismas herramientas) | (Mismas operaciones) | Versión optimizada con correcciones de numeración de líneas y refinamiento de parámetros de corte. |

**Conceptos clave aprendidos:**
- Cambio de herramienta con `M06`
- Ciclo G81: Taladrado simple (feed in, rapid out)
- Ciclo G73/G83: Taladrado profundo con picoteo (peck drilling)
- Comandos Denford G170/G171: Pocket milling (fresado de cavidades)
- Gestión de múltiples herramientas en un solo programa

---

### Serie 2: Letra "S" en placa 3×5" (Febrero 2026)

> **Material:** Aluminio 3"×5"×0.75" · **Profundidad:** 0.250" · **Enfoque:** Interpolación circular

| # | Archivo | Herramienta | Modo | Método | Descripción |
|---|---------|-------------|------|--------|-------------|
| 1 | `O0004_S_Absoluto_R.nc` | 1/2" (Ø0.500") | Absoluto G90 | Radio R | Primer ejercicio de la serie. Contorno de la S con G02/G03 usando el método R en coordenadas absolutas. Base del manual del profesor. **Primera aproximación** con algunos errores de sintaxis. |
| 2 | `O0005_S_Incremental_G91_R.nc` | 1/2" (Ø0.500") | Incremental G91 | Radio R | Mismo patrón que O0004 pero usando coordenadas incrementales (G91). Cada movimiento es relativo a la posición actual. Ejercicio para dominar diferencia entre modos. |
| 3 | `O0006_S_Absoluto_IJ_375.nc` | 3/8" (Ø0.375") | Absoluto G90 | I,J Offset | Cambio de herramienta a 3/8". **Primer uso del método I,J** para definir centro de arco. Contiene errores en cálculo de offsets (ver LEARNING.md). RPM ajustado a 2400 para herramienta menor. |
| 4 | `O0007_S_Incremental_IJ_375.nc` | 3/8" (Ø0.375") | Incremental G91 | I,J Offset | Variante experimental combinando G91 con método I,J. Contiene geometría modificada respecto al diseño original. Ejercicio de exploración. |

**Conceptos clave aprendidos:**
- G02/G03: Interpolación circular horaria y antihoraria
- Método R: Simple pero ambiguo en arcos de 180°
- Método I,J: Offset desde punto inicial al centro (más preciso, estándar industrial)
- G90 vs G91: Coordenadas absolutas vs incrementales
- Relación diámetro herramienta ↔ RPM (herramientas pequeñas = RPM altos)

---

## 📐 Dimensiones y Especificaciones

### Ejercicio Cilindros (O0002/O0003)
```
Material:      Aluminio 120mm × 80mm × 25mm
Patrón:        Matriz 5 columnas × 2 filas
Espaciado:     20mm entre centros (horizontal), 50mm (vertical)
Diámetro cil:  Ø10mm
Profundidad:   22mm desde superficie

Herramientas:
- T01: Broca centros Ø5mm @ 2000 RPM
- T02: Broca Ø10mm @ 1000 RPM
- T03: Cortadora Ø9.5mm @ 1000 RPM
```

### Ejercicio Letra S (O0004-O0007)
```
Material:          Aluminio 3" × 5" × 0.75"
Radio grande:      R 1.5" (semicírculos principales)
Radio pequeño:     R 0.75" (transiciones)
Profundidad:       Z -0.250"
Origen:            Esquina inferior izquierda

Herramientas:
- Fresa 1/2": 2000 RPM, F50-100 IPM
- Fresa 3/8": 2400 RPM, F50-80 IPM
```

---

## 🧠 Conceptos Fundamentales

### G02 / G03 — Interpolación Circular
| Comando | Dirección | Vista desde arriba | Uso común |
|---------|-----------|-------------------|-----------|
| `G02` | Horario (CW) | ↻ | Arcos cóncavas, transiciones internas |
| `G03` | Antihorario (CCW) | ↺ | Arcos convexas, contornos externos |

### Métodos para Definir Arcos

**Método R (Radio)** — Simple, intuitivo, didáctico
```gcode
G03 X1.5 Y0 R1.5
```
- ✅ Fácil de entender y escribir manualmente
- ✅ Ideal para aprendizaje inicial
- ⚠️ Ambiguo en arcos de exactamente 180° (requiere signo)
- ⚠️ No usado por software CAM profesional

**Método I,J (Offset al Centro)** — Preciso, profesional, estándar
```gcode
G03 X1.5 Y0 I0.75 J-0.75
```
- `I` = Distancia en X desde **punto de inicio** al centro
- `J` = Distancia en Y desde **punto de inicio** al centro
- ✅ Sin ambigüedad, siempre preciso
- ✅ Estándar en industria y software CAM
- ⚠️ Requiere cálculo manual del centro

**Fórmula de cálculo I,J:**
```
Para semicírculo de (X₁,Y₁) a (X₂,Y₂):

Centro: X_c = (X₁ + X₂) / 2
        Y_c = (Y₁ + Y₂) / 2

Luego:  I = X_c - X₁
        J = Y_c - Y₁
```

### G90 vs G91 — Sistemas de Coordenadas
```gcode
G90   # Absoluto: todas las coordenadas desde el origen (0,0)
      # Ejemplo: si estoy en (2,3) y programo G01 X5 Y7
      # → Voy a posición absoluta (5,7)

G91   # Incremental: coordenadas desde posición actual
      # Ejemplo: si estoy en (2,3) y programo G01 X3 Y4
      # → Me muevo +3 en X y +4 en Y
      # → Posición final: (5,7)
```

### Ciclos Fijos (Denford/FANUC)
| Código | Nombre | Operación | Uso |
|--------|--------|-----------|-----|
| `G81` | Taladrado simple | Avance → profundidad → retracción rápida | Agujeros pasantes o poco profundos |
| `G82` | Taladrado con pausa | Igual que G81 + pausa en fondo | Mejorar acabado en fondo de agujero |
| `G73` | Picoteo alta velocidad | Múltiples entradas sin retracción completa | Taladrado profundo en aluminio |
| `G83` | Picoteo completo | Retracción total entre cada picoteo | Taladrado muy profundo, evacuación de viruta |
| `G80` | Cancelar ciclo | Desactiva cualquier ciclo activo | **Obligatorio** antes de cambiar herramienta |

### Comandos Denford Específicos
```gcode
G170  # Define geometría de pocket (cavidad a fresar)
      # Parámetros: R (radio), P (tipo), Q (capa), X/Y (centro), Z (profundidad)
      # I/J (dimensiones), K (incremento Z)

G171  # Ejecuta fresado del pocket definido en G170
      # Parámetros: P (diámetro herramienta), S (RPM), R (radio acabado)
      # F (avance), B (avance rápido), J (tolerancia)
```

---

## ⚙️ Parámetros de Corte Utilizados

### Ejercicios Cilindros (O0002/O0003)
| Herramienta | Diámetro | Material | Operación | RPM | Avance (F) | Notas |
|-------------|----------|----------|-----------|-----|------------|-------|
| Broca centros | Ø5mm | HSS | Centrado | 2000 | F100 mm/min | Entrada y salida rápida |
| Broca | Ø10mm | HSS | Taladrado profundo | 1000 | F80 mm/min | Ciclo G73 con Q5 (picoteo 5mm) |
| Cortadora | Ø9.5mm | Carburo | Fresado pocket | 1000→2000 | F12 mm/min | G170/G171, múltiples pasadas |

### Ejercicios Letra S (O0004-O0007)
| Herramienta | Diámetro | RPM | Avance XY | Avance Z | Profundidad | Pasadas |
|-------------|----------|-----|-----------|----------|-------------|---------|
| Fresa plana | 1/2" (Ø12.7mm) | 2000 | F50 IPM | F100 IPM | -0.250" | 1 (didáctico) |
| Fresa plana | 3/8" (Ø9.5mm) | 2400 | F50 IPM | F80 IPM | -0.250" | 1 (didáctico) |

> 📌 **Nota:** Estos parámetros son didácticos para simulación. En producción real se usarían múltiples pasadas (DOC menor) y velocidades optimizadas por material.

---

## 📷 Simulaciones y Resultados

### Matriz de Cilindros
- ✅ **O0002_Cilindros_v1**: Simulación 2D muestra patrón 5×2 correcto
- ✅ **O0003_Cilindros_v2**: Vista 3D confirma profundidad de cilindros

### Letra S
| Programa | Simulación 2D | Simulación 3D | Estado |
|----------|---------------|---------------|--------|
| O0004 — S Absoluta R | Contorno visible | Forma de S reconocible | ✅ Funcional con errores menores |
| O0005 — S Incremental R | G91 ejecuta correctamente | Geometría coincide con O0004 | ✅ Validado |
| O0006 — S I,J 3/8" | Trayectoria desviada | Forma no coincide con diseño | ⚠️ Errores de cálculo I,J |
| O0007 — S Experimental | Geometría modificada | Patrón alternativo | ℹ️ Exploración, no validado |

---

## 📌 Notas Técnicas y Limitaciones

### Sobre el Simulador Denford FANUC Milling v1.96
- Los archivos `.nc` son directamente cargables en el simulador
- Directiva de material: `[BILLET X___ Y___ Z___` (específica Denford)
- Directiva de herramienta: `[TOOLDEF T## D___` (específica Denford)
- Los comandos M están **comentados** en ejercicios didácticos ya que el simulador no requiere control físico de husillo/refrigerante
- ⚠️ **En máquina real** los comandos M06, M03, M08, M09, M05, M30 son **obligatorios**

### Diferencias: Código Didáctico vs Profesional

| Aspecto | Código Didáctico (estos ejercicios) | Código Profesional |
|---------|--------------------------------------|-------------------|
| **Objetivo** | Aprender comandos y sintaxis | Producción eficiente y segura |
| **Pasadas** | 1 pasada a profundidad total | Múltiples pasadas incrementales |
| **Seguridad** | Comandos M mínimos o comentados | Inicialización completa G21/G17/G40/G80/G90, todos los M activos |
| **Velocidades** | Valores conservadores fijos | Optimizadas por material/herramienta |
| **Estructura** | ~30-50 líneas, enfoque en geometría | ~80-150 líneas, headers, checks, retracción |
| **Finalización** | A veces incompleta | Siempre: retracción Z, M05, M09, G28, M30 |

### Errores Comunes Encontrados (ver `LEARNING.md`)
1. ❌ Cálculo incorrecto de I,J (usar radio en lugar de offset)
2. ❌ Comandos M comentados con paréntesis `(M03 S2000`
3. ❌ Números de línea duplicados (N125 aparece 2 veces)
4. ❌ Comandos incompletos (G01 sin coordenadas)
5. ❌ Falta de retracción/finalización segura

---

## 🎓 Progreso de Aprendizaje

### ✅ Conceptos Dominados
- [x] Interpolación lineal (G00/G01)
- [x] Interpolación circular (G02/G03) con método R
- [x] Diferencia entre G90 (absoluto) y G91 (incremental)
- [x] Ciclos fijos básicos (G81, G83)
- [x] Cambio de herramienta (M06, T##)
- [x] Comandos Denford específicos (G170/G171)

### 🔄 En Progreso
- [ ] Método I,J para arcos (requiere más práctica en cálculo manual)
- [ ] Compensación de radio de herramienta (G41/G42)
- [ ] Estructuras de programa completas con seguridad
- [ ] Optimización de parámetros de corte

### 🎯 Próximos Pasos
1. Dominar cálculo de I,J con ejercicios adicionales
2. Implementar múltiples pasadas en lugar de profundidad total
3. Añadir secuencias completas de inicialización y finalización
4. Estudiar compensación G41/G42 para precisión dimensional
5. Transición a generación de código con software CAM

---

## 📚 Recursos de Referencia

Todos los recursos están en la carpeta `recursos/`:

### Cheatsheets (Referencia Rápida)
- `Cheatsheet_CNC_Torno_Fresa.png` — Comandos G/M organizados por categoría
- `Cheatsheet_Denford_Fanuc_v1.png` — Tabla de comandos específicos Denford
- `Cheatsheet_Denford_Fanuc_v2.png` — Diagrama visual de parámetros y ejes
- `Cheatsheet_Programacion_CNC.png` — Sintaxis y estructura de bloques
- `Cheatsheet_Denford_Fanuc.docx` — Versión editable para anotaciones
- `G_code_Fanuc.html` — Guía interactiva HTML con ejemplos

### Guías Completas
- `Guia_Referencia_CNC.pdf` — Manual de programación CNC estándar ISO
- `Guía_Rápida_Código_G.pdf` — Resumen de comandos con sintaxis

### Material del Profesor
- `Manual/` — 9 imágenes JPEG con ejercicios, tablas de interpolación, ciclos de barrenado

---

## 🔗 Enlaces a Documentación Adicional

- [LEARNING.md](../LEARNING.md) — Bitácora completa de aprendizaje con errores y soluciones
- [Guía Profesional de Torno](../../1.Torno-Fresado/recursos/Guia_Profesional_Torno.md) — Operaciones de torno convencional
- [README Principal](../../README.md) — Estructura completa del repositorio

---

**Última actualización:** 17 de Febrero 2026 | CECATI No. 17  
**Estado:** Ejercicios didácticos en progreso | Transición hacia mejores prácticas industriales