# 2.1 Torno CNC

Programación CNC para torno paralelo de control numérico (*CNC lathe*) bajo controlador FANUC. Serie temática basada en piezas de ajedrez como progresión didáctica de complejidad geométrica.

---

## Estado actual

3 ejercicios completados (peón, torre, caballo) con código + simulación verificada. 4 ejercicios pendientes (rey, reyna, alfil, torre-v2) con plano técnico recibido — programación pendiente conforme avanza el curso.

---

## Lo último completado

- **Marzo 2026** — Ejercicio 03 *Caballo* (`O0003`) — pieza con perfil curvo complejo.
- **Marzo 2026** — Ejercicio 02 *Torre* (`O0002`) — perfil escalonado.
- **Marzo 2026** — Ejercicio 01 *Peón* (`O0001`) — pieza inicial de la serie.

---

## Concepto de la serie: piezas de ajedrez

La serie utiliza las 6 piezas del ajedrez (peón, torre, caballo, alfil, rey, reyna) como progresión didáctica. Cada pieza incrementa complejidad geométrica:

| Pieza | Complejidad | Operaciones clave |
|---|---|---|
| **Peón** | Básica | Cilindrado escalonado, refrentado |
| **Torre** | Media | Perfil escalonado con detalles geométricos |
| **Caballo** | Alta | Perfiles curvos, interpolación circular |
| **Alfil** | Media-alta | Perfil cónico con detalles |
| **Rey / Reyna** | Avanzada | Geometría compleja, múltiples cambios de herramienta |
| **Torre-v2** | Refinamiento | Variante mejorada de la Torre |

La elección temática **no es decorativa** — facilita la comunicación en clase ("trabaja en el caballo") y crea una serie reconocible para portafolio.

---

## Estructura de carpetas

```
Torno-CNC/
├── ejercicio-01-peon/
│   ├── codigo-g/        # Programa O0001
│   ├── planos/          # Plano técnico
│   └── simulaciones/    # Capturas Denford
├── ejercicio-02-torre/
├── ejercicio-03-caballo/
├── ejercicio-04-rey/         # Solo plano (pendiente programar)
├── ejercicio-05-reyna/       # Solo plano (pendiente programar)
├── ejercicio-06-alfil/       # Solo plano (pendiente programar)
├── ejercicio-07-torre-v2/    # Solo plano (pendiente programar)
└── README.md
```

---

## Ejercicios de la serie

### Ejercicio 01 — Peón ✅

**Programa:** `O0001-figura-1.nc`
**Plano:** `1.0(Marzo-04).png`
**Estado:** Completado, simulación verificada en Denford FANUC Turning v1.42.

Pieza inicial de la serie. Establece la base técnica: setup del programa, cero pieza, cambio de herramienta, ciclo básico de cilindrado.

**Operaciones realizadas:**
- Refrentado de cara frontal (*facing*).
- Cilindrado escalonado con cambio de diámetro.
- Cambio de herramienta T01 → T02 entre operaciones.

**Aprendizaje técnico:**
- Estructura mínima de programa FANUC: cabecera, bloque principal, fin (`M30`).
- Importancia de la posición de retorno seguro antes del cambio de herramienta.
- Verificación visual de la trayectoria en cada paso de simulación (5 capturas: cabeza, cambio de herramienta, desbastes, pieza completa).

---

### Ejercicio 02 — Torre ✅

**Programa:** `O0002.nc`
**Plano:** `2.0(Marzo).png`
**Estado:** Completado, simulación verificada (vista perfil + vista 3D).

Pieza con perfil escalonado pronunciado, característica visual de la torre de ajedrez (almenas).

**Operaciones realizadas:**
- Cilindrado en múltiples diámetros.
- Generación de detalles geométricos del perfil.
- Manejo de transiciones entre pasos.

**Aprendizaje técnico:**
- Planificación de pasadas de desbaste manual antes de acabado.
- Consideración del orden de operaciones para minimizar movimientos improductivos.

> **Nota didáctica:** El programa usa estrategia de desbaste manual (sin ciclo G70/G71). Esto es **intencionalmente didáctico** — comprender qué hace internamente un ciclo automático antes de invocarlo. La versión profesional industrial usaría G71 para desbaste y G70 para acabado.

---

### Ejercicio 03 — Caballo ✅

**Programa:** `O0003.nc`
**Plano:** `3.0(Marzo).png`
**Estado:** Completado, simulación de acabado verificada.

Pieza con perfiles curvos — primera vez que se introducen arcos significativos en torno CNC.

**Operaciones realizadas:**
- Cilindrado de bases.
- Interpolación circular para perfil del caballo.
- Detalles geométricos del cuello/cabeza.

**Aprendizaje técnico:**
- Uso de G02/G03 en torno (los signos y direcciones difieren respecto a fresa).
- Cálculo de coordenadas de inicio y fin de arco.
- Importancia del plano de trabajo en torno (XZ vs XY).

---

### Ejercicio 04 — Rey ⏳

**Plano recibido:** `4.0(Marzo).png`
**Estado:** Programación pendiente.

Pieza con cabezal complejo característico del rey. Esperada introducción de operaciones más sofisticadas.

---

### Ejercicio 05 — Reyna ⏳

**Plano recibido:** `5.0(Marzo).png`
**Estado:** Programación pendiente.

Pieza con corona escalonada, similar al rey pero con perfil distintivo.

---

### Ejercicio 06 — Alfil ⏳

**Plano recibido:** `6.0(Marzo).png`
**Estado:** Programación pendiente.

Pieza con perfil cónico característico y detalle superior.

---

### Ejercicio 07 — Torre-v2 ⏳

**Plano recibido:** `7.0(Marzo).png`
**Estado:** Programación pendiente.

Variante refinada del ejercicio 02. Probable enfoque en optimización del programa original.

---

## Glosario EN/ES — específico de torno CNC

Terminología adicional al glosario general de [`2.CNC/README.md`](../README.md), específica del torno.

| Inglés | Español | Nota |
|---|---|---|
| *CNC lathe* / *CNC turning center* | Torno CNC / centro de torneado | Las versiones de mayor capacidad incluyen herramientas motorizadas |
| *Turret* | Torreta | Sistema de cambio automático de herramientas |
| *Live tooling* | Herramienta motorizada | Permite fresado en torno (multi-eje) |
| *Sub-spindle* | Contrahusillo | Husillo opuesto para piezas de doble cara |
| *Bar feeder* | Alimentador de barra | Sistema de avance automático para producción en serie |
| *Constant surface speed* (G96) | Velocidad superficial constante | Control automático de RPM según diámetro |
| *Roughing cycle* (G71/G72) | Ciclo de desbaste | Genera múltiples pasadas automáticamente |
| *Finishing cycle* (G70) | Ciclo de acabado | Pasada final con perfil exacto |
| *Threading cycle* (G76) | Ciclo de roscado | Roscado automático con buril |
| *Grooving cycle* (G75) | Ciclo de ranurado | Apertura de canales |
| *Drilling cycle* (G74) | Ciclo de taladrado | Taladrado axial con peck drilling |
| *Chip breaker* | Rompevirutas | Geometría del inserto que fragmenta la viruta |

---

## Conexión con torno convencional

Los ejercicios de Torno-CNC son la **versión programada** de las operaciones que se ejecutan manualmente en `1.torno-fresado-convencional/`. La progresión pedagógica es deliberada:

1. **Torno convencional** → comprender físicamente qué hace cada movimiento.
2. **Torno CNC** → automatizar esa comprensión con código.

Un programador CNC sin experiencia de torno manual genera código sintácticamente correcto pero industrialmente subóptimo (velocidades imposibles, herramientas inapropiadas, secuencias ineficientes). La doble formación es una ventaja competitiva real en industria.

---

## Siguiente paso

1. **Programar ejercicio 04 (Rey)** — siguiente en la secuencia, con plano ya recibido.
2. **Documentar conclusiones de ejercicios 01–03** en bitácora general (`LEARNING.md` en raíz del repo, una vez creada).

---

**Subdisciplina:** Torno CNC (*CNC lathe*)
**Controlador:** FANUC (simulador Denford Turning v1.42)
**Estado:** 3 de 7 ejercicios completados | Serie en desarrollo