# 2. Programación CNC

Práctica de manufactura por control numérico computarizado — *Computer Numerical Control programming*. Curso impartido en CECATI No. 17, Querétaro, dentro del programa de capacitación en maquinado y manufactura. Cubre las dos disciplinas industriales principales: torno CNC (*CNC turning*) y fresado CNC (*CNC milling*).

> **Nota:** Esta carpeta es el contenedor general de programación CNC. El detalle por disciplina está en sus respectivas subcarpetas, cada una con su propio README:
> - [`Torno-CNC/`](./Torno-CNC/README.md) — *CNC lathe programming*
> - [`Fresado-CNC/`](./Fresado-CNC/README.md) — *CNC milling programming*

---

## Estado actual

Curso CNC en progreso activo. Disciplinas en ejecución paralela: torno CNC con serie de ejercicios temáticos (piezas de ajedrez) y fresado CNC con ejercicios de geometría progresiva (cilindros → contornos → cajeados → pocketing).

---

## Lo último completado

- **Marzo 2026** — Ejercicio de fresado *pocketing* con código `O00013` (*Fresado-CNC*).
- **Marzo 2026** — Ejercicio de torno *Caballo* con código `O0003` (*Torno-CNC*).
- **Marzo 2026** — Ejercicio de torno *Torre* con código `O0002` (*Torno-CNC*).

---

## Sobre el curso

**Institución:** CECATI No. 17 — Querétaro
**Simulador principal:** Denford FANUC Milling v1.96 / Denford FANUC Turning v1.42
**Estándar de control:** FANUC ISO 6983 (G-code y M-code estándar industrial)
**Sistema de unidades:** Pulgadas (G20) por convención del curso
**Modalidad:** Plano técnico → planificación de operaciones → escritura de G-code → simulación → verificación.

El simulador Denford FANUC reproduce la lógica de control de máquinas FANUC reales — el estándar de facto en manufactura industrial global. Esto significa que el código G escrito aquí es **transferible directamente** a máquinas industriales con controlador FANUC, Haas, Mazak, Doosan u otros que respeten el estándar ISO 6983.

---

## Estructura

```
2.CNC/
├── Torno-CNC/          # Ejercicios de torno CNC (piezas de ajedrez)
│   └── README.md       # Detalle por ejercicio
├── Fresado-CNC/        # Ejercicios de fresado CNC (geometría progresiva)
│   └── README.md       # Detalle por ejercicio
├── recursos/           # Manuales, cheatsheets, guías de referencia
│   └── README.md       # Catálogo de recursos
└── README.md           # Este archivo
```

---

## Convenciones del repositorio CNC

### Numeración de programas

Programas FANUC siguen convención `Onnnn` (4 dígitos) por estándar ISO 6983. En este repositorio:

| Rango | Asignación |
|---|---|
| `O0001` | Reservado para Torno-CNC ejercicio 01 |
| `O0002`–`O00013` | Asignación cronológica conforme se desarrollan ejercicios |

> **Nota técnica:** En máquinas FANUC reales, el número O identifica el programa en memoria del control. Dos programas con el mismo número O sobrescriben uno al otro. La numeración disciplinada es práctica estándar de industria.

### Estructura de carpetas por ejercicio

Todos los ejercicios siguen la misma estructura tripartita:

```
ejercicio-XX-nombre/
├── codigo-g/        # Programas G-code (.nc)
├── planos/          # Plano técnico de la pieza (PNG/PDF)
└── simulaciones/    # Capturas del simulador Denford (PNG)
```

Esta estructura refleja el flujo industrial: el plano define la pieza, el código define la trayectoria, la simulación verifica antes de ejecutar.

### Extensión de archivos

- **`.nc`** — programa G-code estándar.
- **`.fnc`** — programa Denford FANUC (variante específica del simulador).

> **Buena práctica de industria:** Mantener consistencia de extensiones evita confusión en *post-processors* (postprocesadores) y sistemas DNC (*Direct Numerical Control*).

---

## Glosario EN/ES — terminología CNC general

| Inglés | Español | Nota |
|---|---|---|
| *CNC* (*Computer Numerical Control*) | Control numérico computarizado | Estándar industrial desde los años 70 |
| *G-code* | Código G | Lenguaje de programación de movimiento |
| *M-code* | Código M | Comandos de máquina (ON/OFF, herramienta, refrigerante) |
| *Block* | Bloque | Una línea de programa (`N10 G01 X10. F100`) |
| *Word* | Palabra | Una instrucción dentro del bloque (`G01`, `X10.`) |
| *FANUC* | FANUC | Fabricante japonés de controladores; estándar de facto |
| *ISO 6983* | ISO 6983 | Norma internacional de programación de máquinas-herramienta |
| *Post-processor* | Postprocesador | Software que convierte CAM en G-code para máquina específica |
| *DNC* (*Direct Numerical Control*) | Control numérico directo | Transferencia de programas máquina↔computadora |
| *Tool offset* | Compensación de herramienta | Ajuste por longitud o desgaste |
| *Work offset* | Cero pieza | Origen de coordenadas de la pieza (G54–G59) |
| *Dry run* | Ejecución en seco / simulación | Ejecutar sin material para validar trayectoria |
| *Feed hold* | Pausa de avance | Detener movimiento sin perder posición |
| *Cycle start* | Inicio de ciclo | Botón de arranque del programa |
| *MDI* (*Manual Data Input*) | Entrada manual de datos | Modo para ejecutar bloques sueltos sin programa |
| *Single block* | Bloque por bloque | Ejecutar el programa una línea a la vez |
| *Rapid traverse* | Avance rápido | Movimiento sin corte (G00) |
| *Linear interpolation* | Interpolación lineal | Movimiento recto bajo corte (G01) |
| *Circular interpolation* | Interpolación circular | Arcos (G02 horario, G03 antihorario) |

---

## Recursos compartidos

`recursos/` contiene material de referencia técnica acumulado durante el curso. Ver [`recursos/README.md`](./recursos/README.md) para catálogo detallado. Contenido principal:

- **`guia-maestria-programacion-cnc.pdf`** — guía completa de códigos G y M (torno y fresa).
- **`lenguaje-cnc-codigos-g-m-visual.pdf`** — guía visual con diagramas y ejemplos.
- **`Cheatsheet_CNC_Torno_Fresa.png`** — referencia rápida visual.
- **`Cheatsheet_Denford_Fanuc_v1/v2.png`** — códigos específicos del simulador Denford.
- **`Manual/`** — apuntes manuscritos del instructor (referencia primaria de clase).

---

## Códigos G y M de uso frecuente

Los códigos listados son los efectivamente utilizados en los ejercicios del repo. Para tabla completa, consultar `recursos/`.

### Códigos G (geometría y movimiento)

| Código | Función | Aplica a |
|---|---|---|
| `G00` | Posicionamiento rápido (*rapid traverse*) | Torno + Fresa |
| `G01` | Interpolación lineal con avance | Torno + Fresa |
| `G02` | Interpolación circular horaria (*clockwise*) | Torno + Fresa |
| `G03` | Interpolación circular antihoraria (*counter-clockwise*) | Torno + Fresa |
| `G17`/`G18`/`G19` | Selección de plano (XY/XZ/YZ) | Fresa |
| `G20`/`G21` | Pulgadas / Milímetros | Torno + Fresa |
| `G28` | Retorno a punto de referencia (*home*) | Torno + Fresa |
| `G40` | Cancelar compensación de radio | Fresa |
| `G41`/`G42` | Compensación de radio izquierda/derecha | Fresa (pendiente) |
| `G54` | Selección de cero pieza primario | Torno + Fresa |
| `G70`/`G71` | Ciclo de acabado / desbaste (torno) | Torno (pendiente) |
| `G73`/`G83` | Ciclo de taladrado profundo (peck drilling) | Fresa |
| `G81` | Ciclo de taladrado simple | Fresa |
| `G90`/`G91` | Modo absoluto / incremental | Torno + Fresa |
| `G170`/`G171` | Cajeado circular (específico Denford) | Fresa |

### Códigos M (acciones de máquina)

| Código | Función |
|---|---|
| `M03` | Husillo ON sentido horario (*spindle clockwise*) |
| `M04` | Husillo ON sentido antihorario |
| `M05` | Husillo OFF |
| `M06` | Cambio de herramienta (*tool change*) |
| `M08`/`M09` | Refrigerante ON / OFF |
| `M30` | Fin de programa con rebobinado |
| `M98`/`M99` | Llamada a subrutina / retorno (pendiente) |

---

## Principios de seguridad CNC

Aplicables a toda práctica, simulada o real:

1. **Simular siempre antes de ejecutar.** Una colisión en simulador es gratis; en máquina real cuesta una herramienta o el husillo.
2. **Verificar cero pieza antes de arrancar.** El programa no sabe dónde está la pieza — el operador define el origen con G54.
3. **Validar herramientas en torreta.** El cambio de herramienta automático ejecuta exactamente lo programado; T01 debe ser físicamente la herramienta T01 en la torreta.
4. **Single block en primera ejecución.** Modo bloque-por-bloque permite detectar errores antes de que comprometan la pieza.
5. **Mantener el botón de paro de emergencia (*E-stop*) accesible siempre.**

---

## Siguiente paso

1. **Completar serie de ajedrez en Torno-CNC** — programar ejercicios 04 (rey), 05 (reyna), 06 (alfil), 07 (torre-v2) — actualmente con solo plano recibido.
2. **Introducir compensación de radio (G41/G42) en Fresado-CNC** — siguiente nivel técnico estándar de industria.

---

**Curso institucional:** CECATI No. 17 — Querétaro
**Estado del módulo:** En progreso activo (ambas subdisciplinas)
**Próxima revisión del README:** Al cerrar la serie de ajedrez completa