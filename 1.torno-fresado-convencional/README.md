# 1. Torno y Fresado Convencional

Práctica de manufactura en máquinas convencionales (no CNC) — *manual lathe and milling operations*. Curso impartido en CECATI No. 17, Querétaro, dentro del programa de capacitación en maquinado y manufactura.

> **Nota:** Esta carpeta cubre el curso institucional "Torno y Fresado Convencional". Actualmente el contenido es exclusivamente de torno; las prácticas de fresa convencional se incorporarán cuando inicien.

---

## Estado actual

Curso de torno completado a nivel de prácticas. Todas las piezas listadas han sido maquinadas físicamente, partiendo de plano técnico hasta pieza terminada. Pendiente: documentación fotográfica de piezas terminadas y contenido de fresa convencional.

---

## Lo último completado

- **Marzo 2026** — Pieza *Cañón* + *Base de Cañón* (combinación de operaciones, plano más complejo de la serie).
- **Febrero 2026** — Pieza *Excéntrico* (torneado descentrado).
- **Febrero 2026** — Pieza *Destapador* (forma irregular).
- **Febrero 2026** — Pieza *Flecha1* (flecha sencilla)
- **Febrero 2026** — Pieza *Flecha2* (flecha con roscas encontradas y una ACME )
---

## Sobre el curso

**Institución:** CECATI No. 17 — Querétaro
**Equipo principal:** Torno convencional Harrison M300 (13" × 40") — *engine lathe* (torno paralelo).
**Modalidad:** Práctica directa con plano técnico → maquinado → verificación dimensional.

El flujo de trabajo del curso reproduce el de un taller industrial: el alumno recibe un plano del instructor, planifica las operaciones, selecciona herramienta, ejecuta el maquinado y verifica con instrumentos de medición. Esta secuencia es la que se replica más adelante con CNC, sustituyendo la ejecución manual por código *G-code*.

---

## Operaciones realizadas

| Operación (ES) | Operation (EN) | Descripción técnica |
|---|---|---|
| Cilindrado | *Turning* / *external turning* | Reducción de diámetro exterior con avance longitudinal |
| Refrentado | *Facing* | Generación de superficie plana perpendicular al eje |
| Ranurado | *Grooving* | Apertura de canal interior o exterior con buril de forma |
| Roscado con terraja | *Threading with die* | Generación de cuerda exterior por terraja manual |
| Moleteado | *Knurling* | Texturizado superficial por deformación con rodillo |
| Taladrado en torno | *Drilling on lathe* | Perforación axial con broca montada en contrapunto |
| Tronzado | *Parting / cut-off* | Separación de pieza terminada del material restante |

> **Nota técnica:** El roscado con terraja es la versión manual del roscado. La versión profesional industrial es el roscado con buril (*single-point threading*) o el ciclo automático G76 en CNC, que se trabaja en `2.CNC/Torno-CNC`.

---

## Piezas trabajadas

Cada pieza tiene un flujo documental de tres etapas: **(1)** foto del plano físico recibido del instructor, **(2)** plano digitalizado para referencia limpia, **(3)** fotografía de pieza terminada (pendiente).

| Pieza | Plano físico | Plano digital | Pieza terminada (foto) | Operaciones principales |
|---|---|---|---|---|
| Flecha 1 | ✅ `Foto_planos/Flecha1.jpeg` | ✅ `planos/Flecha1.png` | ⏳ Pendiente | Cilindrado, refrentado |
| Flecha 2 | ✅ `Foto_planos/Flecha2.jpeg` | ✅ `planos/Flecha2.png`, `Flecha2.1.png` | ⏳ Pendiente | Cilindrado, roscado con terraja |
| Excéntrico | ✅ `Foto_planos/Exentrico.jpeg` | ✅ `planos/Exentrico.png` | ⏳ Pendiente | Torneado descentrado |
| Destapador | ✅ `Foto_planos/Destapador.jpeg` | ✅ `planos/Destapador.png` | ⏳ Pendiente | Forma irregular, ranurado |
| Base de lámpara | ✅ `Foto_planos/Base_lampara.jpeg` | — | ⏳ Pendiente | Combinación de operaciones |
| Cañón | — | ✅ `planos/Cañón.png` | ⏳ Pendiente | Cilindrado escalonado, taladrado |
| Base Cañón | — | ✅ `planos/Base_Canon.png` | ⏳ Pendiente | Refrentado, taladrado, roscado |

> **Nota de autenticidad:** Las fotos de planos físicos se conservan deliberadamente — son evidencia de que el trabajo partió de planos institucionales reales del CECATI, no de descargas genéricas.

---

## Galería de piezas terminadas

*Sección pendiente de poblar.*

Cada pieza se fotografiará con el siguiente protocolo:

- **3 ángulos:** superior, perfil lateral, isométrico (45°).
- **Iluminación frontal,** fondo neutro.
- **Foto de detalle** del acabado más crítico (rosca, moleteado, refrentado).
- **Foto con instrumento de medición** (calibrador o micrómetro) cuando la tolerancia sea relevante.

Las imágenes se guardarán en `piezas-terminadas/` con nomenclatura: `{pieza}_{angulo}.jpg` (ej: `flecha2_isometrico.jpg`, `flecha2_detalle-rosca.jpg`).

---

## Estructura de carpetas

```
1.torno-fresado-convencional/
├── Foto_planos/        # Fotos de planos físicos del CECATI
├── planos/             # Planos digitalizados (PNG)
├── practicas/          # Reservada para apuntes de práctica
├── piezas-terminadas/  # Fotografías de piezas maquinadas (a poblar)
├── recursos/           # Manuales y guías de torno
└── README.md
```

---

## Recursos en esta carpeta

`recursos/` contiene material de referencia técnica acumulado durante el curso:

- **`Manual_Torno_Harrison_M300.pdf`** — manual oficial del torno utilizado en CECATI. Referencia para velocidades de corte, especificaciones técnicas y diagrama de transmisión.
- **`Guia_Profesional_Torno.md`** + **`GUÍA_PROFESIONAL_DE_TORNO.pdf`** — guía de buenas prácticas profesionales de torno paralelo.
- **`La_Pirámide_de_la_Maestría_del_Torno.pdf`** — modelo pedagógico de progresión en habilidades de torno (de aprendiz a maestro).
- **`tabla_conversion.png`** — *conversion table* (pulgadas ↔ milímetros, fracciones decimales) — referencia visual rápida.

---

## Instrumentos de medición utilizados

| Instrumento (ES) | Instrument (EN) | Resolución típica |
|---|---|---|
| Vernier / calibrador | *Vernier caliper* | 0.02 mm / 0.001" |
| Comparador de carátula | *Dial indicator* | 0.01 mm |
| Galga de rosca | *Thread gauge / pitch gauge* | — (cualitativo) |
| Escuadra | *Square* | — (cualitativo) |

---

## Glosario EN/ES

Terminología técnica recurrente en torno paralelo, útil para entrevistas y vacantes en industria internacional.

| Inglés | Español | Nota |
|---|---|---|
| *Engine lathe* / *manual lathe* | Torno paralelo / convencional | Operado manualmente, sin control numérico |
| *Chuck* | Mandril / chuck | Sistema de sujeción de la pieza |
| *Tailstock* | Contrapunto | Apoyo opuesto al chuck para piezas largas |
| *Carriage* | Carro principal | Soporte que avanza longitudinalmente |
| *Cross slide* | Carro transversal | Avance perpendicular al eje |
| *Compound rest* | Carro auxiliar / charriot | Carro orientable para conicidades |
| *Tool post* | Torreta portaherramientas | Soporte de herramientas de corte |
| *Cutting tool / lathe bit* | Buril | Herramienta de corte (HSS o widia) |
| *Workpiece* | Pieza de trabajo / pieza | Material en proceso |
| *Stock* | Material en bruto | Material antes de maquinar |
| *Chip* | Viruta | Material removido por el corte |
| *Feed rate* | Avance | Distancia de avance por revolución |
| *Spindle speed* | Velocidad de husillo | RPM del chuck |
| *SFM* (*surface feet per minute*) | Velocidad de corte superficial | Métrica de velocidad de corte real |
| *Tolerance* | Tolerancia | Rango admisible de variación dimensional |
| *Burr* | Rebaba | Material residual no deseado en aristas |

---

## Siguiente paso

1. **Documentar piezas terminadas** — fotografía protocolizada de las 7 piezas según especificación de la sección *Galería de piezas terminadas* (esta semana).
2. **Iniciar contenido de fresa convencional** — cuando arranque el módulo correspondiente del curso, agregar sección dedicada con la misma estructura: operaciones, piezas, glosario.

---

**Curso institucional:** CECATI No. 17 — Querétaro
**Estado del módulo de torno:** Práctica completada, documentación visual pendiente
**Estado del módulo de fresa convencional:** No iniciado