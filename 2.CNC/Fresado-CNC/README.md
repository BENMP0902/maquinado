# 2.2 Fresado CNC

Programación CNC para fresadora de control numérico (*CNC milling*) bajo controlador FANUC. Serie de ejercicios de geometría progresiva: cilindros con multi-herramienta → contornos curvos → cajeados circulares → pocketing rectangular.

---

## Estado actual

4 ejercicios completados con código + simulación verificada. Progresión técnica desde ciclos fijos de taladrado hasta pocketing complejo multi-herramienta. Próximo nivel: compensación de radio (G41/G42) y subrutinas (M98/M99).

---

## Lo último completado

- **Marzo 2026** — Ejercicio *Fresado Pocketing* (`O00013`) — pocketing rectangular con estrategia optimizada.
- **Febrero 2026** — Ejercicio *Cajeado Circular* (`O0008`–`O0010`) — pocketing circular multi-herramienta.
- **Febrero 2026** — Ejercicio *Letra S* — 4 variantes con métodos R e I/J, modos absoluto/incremental.

---

## Concepto de la serie: progresión técnica

A diferencia de Torno-CNC (serie temática de ajedrez), Fresado-CNC progresa por **complejidad técnica**:

| Ejercicio | Concepto técnico introducido |
|---|---|
| **Cilindros** (O0002, O0003) | Multi-herramienta, ciclos fijos de taladrado, comandos Denford |
| **Letra S** (O0004–O0007) | Interpolación circular, método R vs I/J, absoluto vs incremental |
| **Cajeado circular** (O0008–O0010) | Multi-herramienta + pocketing G170/G171 + multi-nivel |
| **Pocketing rectangular** (O00013) | Pocketing manual sin ciclo, estrategia de pasadas |

Cada ejercicio construye sobre los conceptos del anterior.

---

## Estructura de carpetas

```
Fresado-CNC/
├── ejercicios-cilindros/         # O0002, O0003 — multi-herramienta + taladrado
│   ├── codigo-g/
│   ├── planos/
│   └── simulaciones/
├── ejercicios-letra-S/           # O0004–O0007 — 4 variantes de interpolación
│   ├── codigo-g/
│   ├── planos/
│   ├── simulaciones/
│   └── referencia/               # Render del resultado mecanizado esperado
├── ejercicio-cajeado-circular/   # O0008–O0010 — pocketing G170/G171
│   ├── codigo-g/
│   ├── planos/
│   └── simulaciones/
├── ejercicio-fresado-pocketing/  # O00013 — pocketing manual
│   ├── codigo-g/
│   ├── planos/
│   └── simulaciones/
└── README.md
```

---

## Ejercicios completados

### Ejercicio 1 — Matriz de Cilindros ✅

**Programas:** `O0002_Cilindros_v1.nc`, `O0003_Cilindros_v2.nc`
**Planos:** `1.0(Enero).png`, `2.0(Enero).png`
**Material:** Aluminio 120 × 80 × 25 mm
**Patrón:** Matriz 5 × 2 cilindros

Primera incursión en programación multi-herramienta. Establece los fundamentos del cambio de herramienta automático y los ciclos fijos de taladrado.

**Operaciones realizadas:**
- Centrado con broca de centros (G81 — *spot drilling cycle*).
- Taladrado profundo con broca Ø10 mm (G73/G83 — *peck drilling*).
- Generación de cilindros con cortadora Ø9.5 mm (G170/G171 — *pocketing Denford*).

**Aprendizaje técnico:**
- Cambio de herramienta con `M06`.
- Diferencia entre G73 (*peck drilling* con retracción parcial) y G83 (*peck drilling* con retracción total).
- Comandos específicos de Denford G170/G171 — no son estándar FANUC universal, pero sí del simulador.

---

### Ejercicio 2 — Letra S (4 variantes) ✅

**Programas:** `O0004` a `O0007`
**Plano:** `3.0(Febrero).png`
**Material:** Aluminio 3" × 5" × 0.75"
**Profundidad de corte:** 0.250"

Este ejercicio es un **highlight del portafolio**. La misma pieza se programa de **4 formas distintas** para entender los trade-offs entre métodos.

| Programa | Herramienta | Modo | Método de arco |
|---|---|---|---|
| `O0004_S_Absoluto_R.nc` | Fresa 1/2" | Absoluto (G90) | Radio (R) |
| `O0005_S_Incremental_G91_R.nc` | Fresa 1/2" | Incremental (G91) | Radio (R) |
| `O0006_S_Absoluto_IJ_375.nc` | Fresa 3/8" | Absoluto (G90) | Offset I/J |
| `O0007_S_Incremental_IJ_375.nc` | Fresa 3/8" | Incremental (G91) | Offset I/J |

**Aprendizaje técnico:**
- **G02/G03** — interpolación circular horaria/antihoraria.
- **Método R vs método I/J** para definir arcos:
  - **R**: define el radio del arco directamente — sintaxis simple, pero ambiguo en arcos > 180°.
  - **I/J**: define el centro del arco como offset desde el punto inicial — sintaxis más compleja pero **profesionalmente preferida** porque elimina ambigüedad.
- **G90 (absoluto) vs G91 (incremental)** — distintos modelos mentales para el mismo movimiento.
- Relación entre **diámetro de herramienta** y **RPM óptimas**.

> **Nota técnica de industria:** En entornos profesionales se usa predominantemente el método I/J por su falta de ambigüedad geométrica. El método R se considera aceptable solo para arcos < 180°. Los ejercicios O0006 y O0007 representan el método estándar industrial.

> **Sobre los errores documentados:** Los programas O0006 y O0007 contienen errores cometidos durante el aprendizaje (cálculo incorrecto de I/J por confusión entre radio y offset, comandos M comentados con paréntesis, números de línea duplicados). Los archivos se preservan **deliberadamente** — comprender el error es parte del valor pedagógico. Las correcciones se documentarán en el `LEARNING.md` general del repo.

---

### Ejercicio 3 — Cajeado Circular ✅

**Programas:** `O0008_Cajeado_Absoluto_MultiTool.nc`, `O0009_Cajeado_Incremental_v1.nc`, `O0010_Cajeado_Incremental_v2.nc`
**Plano:** `4.0(Febrero).png`
**Material:** Aluminio 4" × 2.5" × 0.501"

Workflow completo multi-herramienta combinando perforado pasante, pocketing circular y contorno multi-nivel. Es el ejercicio más complejo de la serie hasta el momento.

**Secuencia de operaciones:**

| Paso | Herramienta | Operación |
|---|---|---|
| T01 | Broca de centros Ø3/8" | Centrado previo |
| T02 | Broca Ø1/2" | Perforado pasante |
| T03 | Cortadora Ø1/8" | Pocketing circular (G170/G171) |
| T04 | Fresa Ø1/2" | Contorno multinivel |

**Variaciones programadas:**

| Programa | Diferencia clave |
|---|---|
| `O0008` | Modo absoluto G90 en todas las operaciones |
| `O0009` | Modo incremental G91 en operación de perforado |
| `O0010` | Refinamiento de O0009 con corrección de coordenadas |

**Aprendizaje técnico:**
- Coordinación entre operaciones de distinta naturaleza (perforado → pocketing → contorno).
- Cambio de modo G90 ↔ G91 dentro del mismo programa.
- Manejo de múltiples niveles de profundidad en una pieza.

---

### Ejercicio 4 — Fresado Pocketing ✅

**Programa:** `O00013_fresado_pocketing.nc`
**Plano:** `5.0(Marzo).png`
**Estado:** Simulación verificada.

Pocketing rectangular ejecutado **sin ciclo automático**, con estrategia de pasadas manual. Esto es **intencionalmente didáctico** — comprender qué hace internamente un ciclo de pocketing antes de invocarlo automáticamente.

**Aprendizaje técnico:**
- Estrategia de pasadas: *zig-zag* vs *espiral hacia afuera* vs *espiral hacia adentro*.
- Cálculo de *step-over* (avance lateral entre pasadas) en función del diámetro de herramienta.
- Importancia del *step-down* (profundidad por pasada) según material.

> **Nota de industria:** En CAM moderno (Mastercam, Fusion 360) este pocketing se generaría automáticamente. La versión manual es valiosa como ejercicio de comprensión, no como práctica productiva real.

---

## Ciclos fijos utilizados

| Ciclo | Función | Usado en |
|---|---|---|
| `G81` | Taladrado simple (*spot drilling*) | Cilindros |
| `G73` | Taladrado profundo con retracción parcial (*high-speed peck*) | Cilindros |
| `G83` | Taladrado profundo con retracción total (*peck drilling*) | Cilindros |
| `G170` | Pocketing circular — entrada (Denford-específico) | Cilindros, Cajeado circular |
| `G171` | Pocketing circular — parámetros (Denford-específico) | Cilindros, Cajeado circular |

> **Importante:** G170/G171 son **comandos específicos del simulador Denford**. En máquinas FANUC industriales reales, el pocketing circular se programa con macros, ciclos de fabricante (*custom macro*) o se genera por CAM. La sintaxis estándar varía por fabricante.

---

## Glosario EN/ES — específico de fresado CNC

Terminología adicional al glosario general de [`2.CNC/README.md`](../README.md), específica de fresa.

| Inglés | Español | Nota |
|---|---|---|
| *CNC mill* / *machining center* | Fresadora CNC / centro de maquinado | VMC = vertical, HMC = horizontal |
| *Endmill* | Cortador de extremo / fresa de mango | Herramienta primaria de fresado |
| *Flute* | Flauta / canal de viruta | Cantidad afecta evacuación de viruta y RPM |
| *Pocket* | Cajeado / cavidad | Operación de remoción interna de material |
| *Pocketing* | Cajeado / vaciado | Estrategia de generación del pocket |
| *Contour* / *profile* | Contorno / perfil | Trayectoria que sigue el borde de la pieza |
| *Step-over* | Avance lateral | Distancia entre pasadas paralelas |
| *Step-down* | Profundidad por pasada | Z-incremento por nivel |
| *Climb milling* | Fresado en concordancia | Avance en sentido de rotación de herramienta |
| *Conventional milling* | Fresado convencional / en oposición | Avance contra sentido de rotación |
| *Cutter compensation* | Compensación de cortador | Ajuste por radio de herramienta (G41/G42) |
| *Plunge* | Plunge / penetración axial | Entrada vertical en material |
| *Ramp entry* | Entrada en rampa | Entrada angular para distribuir carga |
| *Helical entry* | Entrada helicoidal | Entrada en espiral, ideal para pockets cerrados |
| *Chip load* | Avance por diente | Métrica fundamental de parámetros de corte |
| *Spindle speed* (RPM) | Velocidad de husillo | Calculada desde SFM y diámetro |
| *Feed rate* (IPM/mm/min) | Velocidad de avance | Producto de chip load × dientes × RPM |

---

## Próximo nivel técnico

Conceptos pendientes de introducir en el curso:

- **Compensación de radio (G41/G42)** — permite programar la trayectoria del **borde de la pieza** en lugar del **centro de la herramienta**. Es estándar de industria; sin esto, cada cambio de herramienta requiere recalcular todo el código.
- **Subrutinas (M98/M99)** — permite reutilizar bloques de código (ej: un patrón de agujeros que se repite). Reduce tamaño del programa y errores de transcripción.
- **Variables del sistema (`#`)** — programación paramétrica. Permite generar familias de piezas con un solo programa.
- **Ciclos de roscado con macho (*tapping*)** — `G84` para roscado interior.

---

## Siguiente paso

1. **Introducir compensación de radio** — siguiente concepto técnico a integrar.
2. **Ejercicio con subrutinas** — patrón de agujeros o repeticiones geométricas.

---

**Subdisciplina:** Fresado CNC (*CNC milling*)
**Controlador:** FANUC (simulador Denford Milling v1.96)
**Estado:** 4 ejercicios completados | Serie en desarrollo