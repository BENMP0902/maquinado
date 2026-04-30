# 3. AutoCAD

Diseño técnico 2D — *technical drafting and architectural drawing*. Curso impartido en CECATI No. 17, Querétaro, dentro del programa de capacitación. Cubre desde fundamentos de dibujo técnico hasta planos arquitectónicos completos con instalaciones y estructura.

---

## Estado actual

Curso completado a nivel de proyecto integrador. Proyecto final entregado: serie de 8 planos técnicos de una casa estilo tradicional (arquitectónico, instalaciones, estructural). Pendiente: refinamientos avanzados de presentación (layouts, viewports, ploteo a escala) y proyecto arquitectónico de diseño propio.

---

## Lo último completado

- **Abril 2026** — Plano arquitectónico final entregado (`Plano_Arquitectonico.dwg` + PDF para impresión).
- **Marzo 2026** — Ejercicios de medición (distancia, área, ángulo, radio) — `14-03-26.dwg`.
- **Marzo 2026** — Ejercicios de sombreado y acabado — `07-03-26.dwg`.

---

## Highlight del portafolio: Casa Estilo Tradicional

Proyecto integrador del curso. Serie completa de **8 planos técnicos** de una vivienda unifamiliar, generados desde cero en AutoCAD 2D. Cubre las tres categorías típicas de un proyecto arquitectónico real:

### Planos arquitectónicos

| # | Plano | Contenido principal |
|---|---|---|
| 1 | Casa Estilo Tradicional 2D | Vista general del proyecto |
| 2 | Planta Arquitectónica | Distribución de espacios, dimensiones, ubicación de puertas y ventanas, mobiliario básico |
| 3 | Planta de Techo y Fachada | Estructura de techumbre, pendientes, bajadas pluviales, elevación frontal |
| 4 | Isométrico y Corte Longitudinal | Vista isométrica desde 2D, corte mostrando alturas, niveles, cimentación, losa |

### Planos de instalaciones

| # | Plano | Contenido principal |
|---|---|---|
| 5 | Instalación Hidrosanitaria y Gas | Red de agua fría/caliente, drenaje sanitario y pluvial, línea de gas LP |
| 6 | Instalación Eléctrica | Circuitos de iluminación, contactos, tablero de distribución, acometida |

### Planos estructurales

| # | Plano | Contenido principal |
|---|---|---|
| 7 | Plano Estructural 1 — Cimentación | Trazo de cimientos, zapatas, cadenas de desplante, especificaciones de concreto y acero |
| 8 | Plano Estructural 2 — Superestructura | Castillos, dalas, losas de entrepiso, estructura de techumbre |

> **Nota técnica:** Esta serie reproduce el alcance documental real de un proyecto arquitectónico ejecutivo. En industria, estos 8 planos son el conjunto mínimo que un constructor necesita para ejecutar la obra.

Las imágenes están en `proyecto-final/` con nombres `1.- Casa Estilo Tradicional 2D.jpg` a `8.- Plano Estructural 2 2D.jpg`. El archivo editable es `Plano_Arquitectonico.dwg`.

---

## Sobre el curso

**Institución:** CECATI No. 17 — Querétaro
**Software:** AutoCAD 2024 (licencia educativa Autodesk)
**Modalidad:** Práctica directa con plano técnico → digitalización → entrega en formato profesional.

El curso reproduce el flujo de un *drafter* (dibujante técnico) profesional: recepción de croquis o requerimiento → trazo en AutoCAD con estándares correctos → acotación → impresión a escala. Esta progresión es la base para cualquier disciplina que use planos: arquitectura, manufactura, instalaciones.

---

## Estructura

```
3.autocad/
├── ejercicios/             # Ejercicios cortos (cotas, sombreados, mediciones)
├── planos-dibujos/         # Dibujos didácticos iniciales (estrella, cruz)
├── proyecto-final/         # 8 planos del proyecto arquitectónico integrador
├── recursos/               # Bibliotecas, plantillas, material de teoría del color
└── README.md
```

---

## Recursos en esta carpeta

`recursos/` contiene material de apoyo del curso:

- **`Libreria.dwg`** — biblioteca de símbolos arquitectónicos: mobiliario (camas, mesas, sillas), elementos sanitarios (WC, lavabo, regadera), puertas y ventanas (varias medidas), vegetación. Insertable como bloques en proyectos.
- **`Pie_de_Plano.dwg`** — cajetín técnico normalizado con campos de título, escala, fecha, dibujante, proyecto, logo CECATI y cuadro de revisiones. Plantilla reutilizable.
- **`La Armonía en el Color - Nuevas Tendencias.pdf`** — círculo cromático, combinaciones armónicas (complementarios, análogos, tríadas), psicología del color en arquitectura.
- **`Sensación + Significado y aplicación del color FINAL.pdf`** — percepción visual del color, significado cultural, accesibilidad y contraste.

> **Nota de industria:** AutoCAD es técnico, pero la presentación final de planos involucra criterios estéticos. Los recursos de teoría del color del curso reflejan que un buen *drafter* no solo dibuja correcto, también comunica visualmente.

---

## Convenciones técnicas aplicadas

### Capas (*layers*) por tipo de elemento

Estándar del curso, replicable en cualquier proyecto:

| Capa | Color | Uso |
|---|---|---|
| MUROS | Blanco (7) | Muros estructurales |
| PUERTAS | Rojo (1) | Puertas y abatimientos |
| VENTANAS | Azul (5) | Ventanas y marcos |
| MOBILIARIO | Cyan (4) | Muebles y equipamiento |
| COTAS | Magenta (6) | Dimensiones y acotaciones |
| EJES | Verde (3) | Ejes de trazo (tipo de línea: centro) |
| TEXTO | Blanco (7) | Textos y etiquetas |
| HATCH | Amarillo (2) | Rellenos y sombreados |

### Escalas de impresión

| Tipo de plano | Escala |
|---|---|
| Planta arquitectónica | 1:50 / 1:100 |
| Detalles constructivos | 1:20 / 1:25 |
| Instalaciones | 1:75 / 1:100 |
| Fachadas y cortes | 1:50 / 1:75 |

### Formatos de papel (norma ISO 216)

| Formato | Dimensiones | Uso |
|---|---|---|
| A4 | 210 × 297 mm | Ejercicios, detalles |
| A3 | 297 × 420 mm | Planos individuales |
| A2 | 420 × 594 mm | Plantas completas |
| A1 | 594 × 841 mm | Proyectos integradores |

---

## Glosario EN/ES

Terminología técnica de dibujo asistido por computadora, útil para entrevistas y vacantes en industria internacional.

| Inglés | Español | Nota |
|---|---|---|
| *CAD* (*Computer-Aided Design*) | Diseño asistido por computadora | Categoría general |
| *Drafting* | Dibujo técnico | Específicamente la disciplina del dibujo |
| *Drafter* | Dibujante técnico | Rol profesional |
| *Layer* | Capa | Sistema de organización por elementos |
| *Block* | Bloque | Símbolo o elemento reutilizable |
| *XREF* (*External Reference*) | Referencia externa | Vinculación de archivos DWG |
| *Layout* | Espacio de presentación | Vista para impresión |
| *Viewport* | Ventana gráfica | Vista de modelo dentro del layout |
| *Modelspace* | Espacio modelo | Donde se dibuja a escala 1:1 |
| *Paperspace* | Espacio papel | Donde se compone la impresión |
| *Object Snap (OSNAP)* | Referencia a objetos | Puntos de anclaje (endpoint, midpoint, center) |
| *Polar tracking* | Rastreo polar | Asistente de ángulos |
| *Ortho mode* | Modo ortogonal | Restricción a líneas horizontales/verticales |
| *Hatch* | Sombreado / patrón de relleno | Texturas indicativas (tierra, concreto, etc.) |
| *Plot* | Trazado / impresión | Generar salida final (papel o PDF) |
| *Plot style* | Estilo de impresión | Asignación de colores → grosor de línea |
| *DWG* / *DXF* | (formatos) | DWG nativo Autodesk; DXF intercambio |
| *Annotation* | Anotación | Texto, cotas, marcas técnicas |
| *Dimension* | Cota / dimensión | Indicación numérica de medida |
| *Tolerance* | Tolerancia | Rango admisible (en planos de manufactura) |
| *Title block* | Cajetín / pie de plano | Bloque de información del plano |
| *Scale* | Escala | Relación dibujo:realidad |

---

## Conexión con manufactura

AutoCAD no es una disciplina aislada en este portafolio. El dibujo técnico es la **lengua común** entre quien diseña una pieza y quien la fabrica. Las habilidades adquiridas aquí son transversales:

- **Lectura activa de planos** — saber cómo se construye un plano hace que lo leas con criterio crítico, no como receptor pasivo. Esto se aplica directamente a la programación CNC: entender qué cotas son críticas y cuáles son de referencia.
- **Convenciones de acotación** — los símbolos de tolerancia, GD&T, indicaciones de superficie son los mismos en planos arquitectónicos y de manufactura.
- **Pensamiento espacial 2D ↔ 3D** — manejar planta + corte + isométrico es el mismo músculo mental que se usa en SolidWorks (modelado 3D) y en CNC (visualizar trayectorias).

---

## Siguiente paso

1. **Acotación profesional** — dominar `DIMENSION` con estilos personalizados, tolerancias y notación GD&T básica.
2. **Proyecto arquitectónico de diseño propio** — aplicar todo el conocimiento del curso a una vivienda diseñada desde cero, no replicada de plantilla.

---

**Curso institucional:** CECATI No. 17 — Querétaro
**Estado:** Curso completado a nivel de proyecto integrador
**Software:** AutoCAD 2024