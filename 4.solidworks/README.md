# 4. SolidWorks

Modelado 3D paramétrico — *parametric 3D modeling and assembly design*. Curso impartido en CECATI No. 17, Querétaro. Cubre desde piezas básicas hasta ensamblajes funcionales, con generación de planos técnicos derivados del modelo 3D.

---

## Estado actual

Curso en progreso activo. 15 dibujos completados con modelos 3D + planos técnicos derivados. Cubre piezas básicas, ensamblajes simples, y geometrías progresivamente complejas. Proximidad al objetivo de certificación CSWA (*Certified SolidWorks Associate*).

---

## Lo último completado

- **Marzo 2026** — Dibujo 15: Pinza de Expansión de Doble Cono — pieza con geometría compleja y simetría axial.
- **Marzo 2026** — Dibujo 14: Vela — modelado con superficie curva.
- **Marzo 2026** — Dibujo 13: Candelabro — primera incorporación de modelado decorativo.
- **Marzo 2026** — Dibujo 12: Soporte de Cojinete — pieza mecánica funcional.
- **Marzo 2026** — Dibujo 11: Caja con Lente — combinación de operaciones de extrusión y vaciado.

---

## Concepto del curso: progresión por complejidad

Los ejercicios se numeran en orden de complejidad creciente. Cada dibujo introduce **al menos un concepto técnico nuevo** sobre el anterior. La numeración respeta esta progresión.

| Dibujo | Pieza | Concepto técnico introducido |
|---|---|---|
| 1 | Caja | Extrusión básica (*extrude boss*) |
| 2 | Lápiz | Revolución (*revolve*) y conicidad |
| 3 | (Práctica) | Combinación extrusión + corte |
| 4 | (Práctica) | Patrones lineales y circulares |
| 5 | Caja para CD | Vaciado interior (*shell* / *cut extrude*) |
| 6 | Estuche para CDs | Ensamblaje básico (mating de piezas) |
| 7 | Destapador | Geometría irregular, curvas controladas |
| 8 | Puerta | Múltiples operaciones, bisagras conceptuales |
| 9 | Llave Española | Geometría funcional, ajuste dimensional |
| 10 | Marcador / Resaltador | Modelado de producto comercial |
| 11 | Caja con Lente | Operaciones combinadas (extrusión + vaciado) |
| 12 | Soporte de Cojinete | Pieza mecánica funcional con tolerancias |
| 13 | Candelabro | Modelado decorativo con simetría |
| 14 | Vela | Superficies curvas, *loft* básico |
| 15 | Pinza de Expansión de Doble Cono | Geometría compleja, simetría axial |

> **Nota didáctica:** Cada dibujo numerado tiene típicamente dos archivos: el modelo principal (ej: `Dibujo 11, Caja con Lente.SLDPRT`) y un ejercicio de práctica (ej: `Dibujo 11, Práctica.SLDPRT`). El primero es la pieza guiada por el instructor; el segundo es aplicación independiente del concepto.

---

## Ensamblajes completados

| Ensamblaje | Componentes | Operaciones |
|---|---|---|
| Ensamblaje 1 | Placa + Tornillo | Mate concéntrico, mate coincidente |
| Ensamblaje 2 | Estuche + tapa | Articulación con bisagra conceptual |
| Ensamblaje Portavelas | Vela + Candelabro | Composición vertical, posicionamiento |

Los ensamblajes se guardan como archivos `.SLDASM` y referencian las piezas individuales (`.SLDPRT`). Esta estructura es estándar de industria — los ensamblajes en proyectos reales pueden referenciar cientos de piezas con dependencias.

---

## Sobre el curso

**Institución:** CECATI No. 17 — Querétaro
**Software:** SolidWorks 2024 Education Edition
**Modalidad:** Modelo guiado por instructor → ejercicio de práctica independiente → generación de plano técnico.

El flujo del curso reproduce el *workflow* profesional de un diseñador mecánico: comprender el requerimiento → modelar la pieza → verificar dimensiones → generar planos técnicos para fabricación. Los planos PDF derivados de cada modelo (almacenados en `planos-dibujos/`) son la entrega que recibiría un torneador o operario CNC para fabricar la pieza.

---

## Estructura

```
4.solidworks/
├── modelos-3d-ejercicios/    # Archivos SLDPRT (modelos) y SLDASM (ensamblajes)
├── planos-dibujos/           # Planos técnicos PDF derivados de los modelos
└── README.md
```

> **Nota sobre organización física:** la carpeta `modelos-3d-ejercicios/` actualmente contiene 38 archivos sueltos sin sub-organización por dibujo. Esto funciona para volúmenes pequeños pero se vuelve difícil de navegar al crecer. Una reorganización futura por subcarpeta (`dibujo-01/`, `dibujo-02/`, etc.) facilitaría la consulta — pendiente para sesión de mantenimiento.

---

## Operaciones (*features*) dominadas

Lista descriptiva — no aspiracional. Operaciones efectivamente utilizadas en los dibujos completados:

| Operación (EN) | Operación (ES) | Aplicada en |
|---|---|---|
| *Extrude boss* | Extrusión sólida | Dibujos 1, 5, 8, 11+ |
| *Extrude cut* | Corte por extrusión | Dibujos 5, 7, 11+ |
| *Revolve* | Revolución | Dibujos 2, 13, 14 |
| *Fillet* | Redondeo de aristas | Casi todos los dibujos |
| *Chamfer* | Bisel | Dibujos mecánicos (12, 15) |
| *Mirror* | Simetría | Dibujos 13, 15 |
| *Linear pattern* | Patrón lineal | Dibujos 4, 11 |
| *Circular pattern* | Patrón circular | Dibujos 4, 13 |
| *Shell* | Vaciado | Dibujos 5, 8 |
| *Mate (concentric, coincident)* | Restricción de ensamblaje | Ensamblajes |

Operaciones **no aplicadas todavía** y que vienen en niveles más avanzados:

- *Loft* — transición entre perfiles distintos.
- *Sweep* — extrusión a lo largo de trayectoria.
- *Sheet metal* — diseño de chapa metálica.
- *Surface modeling* — modelado por superficies.
- *SolidWorks CAM* — generación de G-code desde modelo (puente a CNC).

---

## Convención de archivos

El curso utiliza una convención de naming particular que vale la pena documentar:

```
DD-MM-YY(Dibujo N, [descripción]).SLDPRT
```

Ejemplos reales:
- `14-03-26(Dibujo 11, Caja con Lente).SLDPRT`
- `21-03-26(Porta-vela).SLDPRT`

> **Decisión técnica:** Esta nomenclatura es del curso (impuesta por el flujo de entrega), no auto-elegida. Refleja la fecha de la sesión + número de dibujo + descripción. En un repositorio profesional propio se preferiría `dibujo-11-caja-con-lente.SLDPRT` (kebab-case sin caracteres especiales). La inconsistencia entre la convención del curso y la convención profesional es un trade-off conocido — preservo los nombres originales por trazabilidad con el material del CECATI.

---

## Ruta hacia certificación CSWA

**CSWA** (*Certified SolidWorks Associate*) es la certificación de entrada de Dassault Systèmes. Validable globalmente, vigente en industria.

**Requisitos cubiertos por el curso actual:**
- Modelado de piezas con extrusión, revolución, corte.
- Generación de planos técnicos con vistas y cotas.
- Ensamblajes básicos con restricciones (*mates*).

**Pendientes para CSWA:**
- Manejo de configuraciones (*configurations*) en una misma pieza.
- Patrones complejos (*patterns* con omisiones, *driven dimensions*).
- Cálculo de propiedades de masa y centro de gravedad.

**Pendientes para CSWP** (*Professional*, siguiente nivel):
- *Loft* y *sweep* avanzados.
- Diseño de chapa metálica.
- Soldaduras (*weldments*).
- Ensamblajes top-down con relaciones paramétricas.

La licencia educativa Autodesk-equivalente de SolidWorks incluye vouchers de certificación. Aplicar en momento adecuado del curso.

---

## Glosario EN/ES

Terminología SolidWorks específica, útil para documentación técnica y entrevistas internacionales.

| Inglés | Español | Nota |
|---|---|---|
| *Part* | Pieza | Archivo `.SLDPRT` |
| *Assembly* | Ensamblaje | Archivo `.SLDASM` |
| *Drawing* | Plano técnico | Archivo `.SLDDRW` |
| *Sketch* | Croquis / boceto 2D | Base de toda operación 3D |
| *Feature* | Operación | Acción que modifica el sólido |
| *Feature tree* | Árbol de operaciones | Historial editable de la pieza |
| *Mate* | Restricción de ensamblaje | Define relación entre dos piezas |
| *Fully defined* | Totalmente definido | Sketch sin grados de libertad |
| *Under-defined* | Sub-definido | Sketch con grados de libertad pendientes |
| *Over-defined* | Sobre-definido | Sketch con restricciones contradictorias |
| *Reference geometry* | Geometría de referencia | Planos, ejes, puntos auxiliares |
| *Configuration* | Configuración | Variante de una misma pieza |
| *Boss* | Saliente / extrusión positiva | Adición de material |
| *Cut* | Corte | Remoción de material |
| *Fillet* | Redondeo | Suavizado de arista |
| *Chamfer* | Bisel | Corte de arista a 45° |
| *Shell* | Vaciado | Hueco interior |
| *Pattern* | Patrón | Repetición de feature |
| *Loft* | Loft | Transición entre perfiles |
| *Sweep* | Barrido | Extrusión a lo largo de trayectoria |
| *Mass properties* | Propiedades físicas | Masa, volumen, centro de gravedad |
| *Bill of Materials* (BOM) | Lista de materiales | Resumen de componentes de un ensamblaje |

---

## Conexión con CNC y manufactura

SolidWorks no es una disciplina aislada. Su valor real para el portafolio se materializa en dos puntos:

### 1. Plano de fabricación derivado del modelo

Los archivos PDF en `planos-dibujos/` son **planos técnicos generados desde el modelo 3D**. Esto reproduce el flujo profesional moderno: la fuente de verdad es el modelo paramétrico; los planos se derivan de él. Cuando una cota cambia en el modelo, el plano se actualiza automáticamente.

Esto es **superior** al flujo tradicional de AutoCAD (donde modelo y plano son la misma cosa). En proyectos profesionales de manufactura, SolidWorks → planos derivados es el estándar.

### 2. Puente al CAM (futuro)

**SolidWorks CAM** es el módulo que convierte un modelo 3D en G-code automáticamente. Es el momento donde tres disciplinas de este portafolio convergen:

```
SolidWorks (diseño) → SolidWorks CAM (generación de G-code) → Máquina CNC (ejecución)
```

Cuando llegue a integrar este flujo, será un hito significativo de portafolio — comunica al reclutador que entiendo el ciclo completo *design → manufacture*, no solo piezas aisladas.

Esta integración aún no se ha realizado en el curso. Está en horizonte cercano.

---

## Siguiente paso

1. **Continuar serie de dibujos** — el curso introduce ejercicios cada vez más complejos. Próximos esperados: *loft*, *sweep*, configuraciones múltiples.
2. **Iniciar exploración de SolidWorks CAM** — diseñar una pieza simple, generar su G-code, comparar contra programa manual escrito en `2.CNC/`.

---

**Curso institucional:** CECATI No. 17 — Querétaro
**Estado:** Curso en progreso — 15 dibujos completados
**Software:** SolidWorks 2024 Education Edition
**Certificación objetivo:** CSWA (*Certified SolidWorks Associate*)