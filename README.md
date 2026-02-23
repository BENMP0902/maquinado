# 🔧 Maquinado - CECATI 17

Repositorio personal de aprendizaje en **manufactura, diseño CAD/CAM y programación CNC**.  
Documenta mi formación completa en CECATI No. 17 desde nivel básico hasta prácticas profesionales.

> 📚 **Filosofía del repositorio:** Este es un portafolio de aprendizaje progresivo. Los ejercicios iniciales son didácticos y enfocados en comprender fundamentos. A medida que avanzo, el código y las prácticas evolucionan hacia estándares profesionales. El archivo [`LEARNING.md`](LEARNING.md) documenta errores, soluciones y progreso técnico.

---

## 📂 Estructura del Repositorio

```
maquinado/
├── 1.Torno-Fresado/          # Prácticas de torno convencional
│   ├── Foto_planos/          # 5 fotos de planos técnicos
│   ├── planos/               # 5 planos digitalizados (PNG)
│   ├── practicas/            # (Carpeta para futuras prácticas)
│   └── recursos/             # Guías y manuales de torno
│       ├── Guia_Profesional_Torno.md
│       └── Manual_Torno_Harrison_M300.pdf
│
├── 2.CNC/                    # Programación CNC - FANUC
│   ├── ejercicios-cilindros/
│   │   ├── O0002_Cilindros_v1.nc
│   │   ├── O0003_Cilindros_v2.nc
│   │   ├── planos/           # Planos técnicos ejercicios
│   │   └── simulaciones/     # Capturas 2D/3D Denford
│   ├── ejercicios-letra-S/
│   │   ├── O0004_S_Absoluto_R.nc
│   │   ├── O0005_S_Incremental_G91_R.nc
│   │   ├── O0006_S_Absoluto_IJ_375.nc
│   │   ├── O0007_S_Incremental_IJ_375.nc
│   │   ├── planos/
│   │   ├── simulaciones/     # 8 imágenes 2D/3D
│   │   └── referencia/       # Renders y resultados esperados
│   ├── ejercicio-cajeado-circular/
│   │   ├── O0008_Cajeado_Absoluto.nc
│   │   ├── O0009_Cajeado_Incremental_v1.nc
│   │   ├── O0010_Cajeado_Incremental_v2.nc
│   │   ├── planos/
│   │   └── simulaciones/
│   ├── planos/               # Planos generales CNC
│   ├── recursos/             # Cheatsheets, manuales, guías
│   │   ├── Cheatsheet_CNC_Torno_Fresa.png
│   │   ├── Cheatsheet_Denford_Fanuc_v1.png
│   │   ├── Cheatsheet_Denford_Fanuc_v2.png
│   │   ├── Cheatsheet_Denford_Fanuc.docx
│   │   ├── G_code_Fanuc.html
│   │   ├── Guia_Referencia_CNC.pdf
│   │   └── Manual/           # 9 imágenes del profesor
│   ├── simulador-denford-fanuc/
│   └── README.md
│
├── 3.autocad/                # Diseño técnico 2D
│   ├── ejercicios/
│   │   ├── Dibujo_1_Estrella.pdf
│   │   ├── Dibujo_2_Cruz_Invertida.dwg
│   │   ├── Libreria.dwg      # Biblioteca de símbolos
│   │   └── Pie_de_Plano.dwg  # Plantilla de cajetín
│   ├── proyectos/
│   │   └── planos-arquitectonicos/
│   │       ├── 1_Casa_Estilo_Tradicional_2D.jpg
│   │       ├── 2_Planta_Arquitectonica_2D.jpg
│   │       ├── 3_Planta_Techo_Fachada_2D.jpg
│   │       ├── 4_Isometrico_Corte_Longitudinal_2D.jpg
│   │       ├── 5_Instalacion_Hidrosanitario_Gas_2D.jpg
│   │       ├── 6_Instalacion_Electrica_2D.jpg
│   │       ├── 7_Plano_Estructural_1_2D.jpg
│   │       └── 8_Plano_Estructural_2_2D.jpg
│   ├── recursos/
│   │   ├── La_Armonia_en_el_Color.pdf
│   │   └── Sensacion_Aplicacion_Color.pdf
│   └── README.md
│
├── 4.solidworks/             # Modelado 3D y ensamblajes
│   ├── ejercicios/
│   │   ├── Ensamblaje1.SLDASM
│   │   ├── Placa.SLDPRT
│   │   ├── Practica_2.SLDPRT
│   │   └── Tornillo.SLDPRT
│   ├── planos/               # 6 PDFs de planos de piezas
│   ├── modelos-3d/           # (Para futuros modelos)
│   └── README.md
│
├── 5.recursos/               # Recursos generales
│   ├── apuntes/              # (Para apuntes de clase)
│   ├── INVENTARIO_COMPLETO.md
│   ├── GUÍA_PROFESIONAL_DE_TORNO.pdf
│   ├── La_Pirámide_de_la_Maestría_del_Torno.pdf
│   └── tabla_conversion.png
│
├── LEARNING.md               # Bitácora de aprendizaje (errores y soluciones)
├── README.md                 # Este archivo
└── .gitignore                # Archivos ignorados por Git
```

**Total actual:** ~80+ archivos organizados | **Última actualización:** Febrero 2026

---

## 📚 Contenido por Área de Estudio

### 🔩 1. Torno Convencional

**Estado:** ✅ Prácticas básicas completadas

**Piezas maquinadas:**
- Flecha simple (cilindrado, refrentado)
- Flecha roscada (roscado exterior)
- Excéntrico (torneado descentrado)
- Destapador (forma irregular)
- Base de lámpara (combinación de operaciones)

**Operaciones dominadas:**
- Cilindrado exterior
- Refrentado
- Ranurado
- Roscado con terraja
- Moleteado
- Taladrado en torno

**Recursos disponibles:**
- [Guía Profesional de Torno](1.Torno-Fresado/recursos/Guia_Profesional_Torno.md) (33KB)
- Manual Harrison M300 (PDF completo)
- 10 planos técnicos con dimensiones

---

### ⚙️ 2. Programación CNC

**Estado:** 🔄 En progreso activo | **Simulador:** Denford FANUC Milling v1.96

#### Serie Completada 1: Matriz de Cilindros
**Ejercicios:** O0002, O0003  
**Tipo:** Multi-herramienta (broca centros, broca Ø10mm, cortadora Ø9.5mm)  
**Operaciones:** Centrado (G81), Taladrado profundo (G73/G83), Pocket milling (G170/G171)  
**Material:** Aluminio 120×80×25mm  
**Patrón:** 5×2 cilindros

**Conceptos aprendidos:**
- Cambio de herramienta (M06)
- Ciclos fijos de taladrado
- Comandos Denford G170/G171
- Gestión de múltiples operaciones

---

#### Serie Completada 2: Letra S (4 variaciones)
**Ejercicios:** O0004, O0005, O0006, O0007  
**Material:** Aluminio 3"×5"×0.75"  
**Profundidad:** 0.250"

| Programa | Herramienta | Modo | Método Arco | Descripción |
|----------|-------------|------|-------------|-------------|
| **O0004** | Fresa 1/2" | Absoluto G90 | Radio R | Base del profesor, primera aproximación |
| **O0005** | Fresa 1/2" | Incremental G91 | Radio R | Coordenadas relativas, mismo patrón |
| **O0006** | Fresa 3/8" | Absoluto G90 | I,J Offset | Primer uso de método I,J (con errores) |
| **O0007** | Fresa 3/8" | Incremental G91 | I,J Offset | Variante experimental |

**Conceptos aprendidos:**
- G02/G03 (interpolación circular CW/CCW)
- Método R vs método I,J para arcos
- G90 (absoluto) vs G91 (incremental)
- Relación diámetro herramienta ↔ RPM

**Errores documentados:**
- Cálculo incorrecto de I,J (confusión radio vs offset)
- Comandos M comentados con paréntesis
- Números de línea duplicados
- Ver [`LEARNING.md`](LEARNING.md) para análisis completo

---

#### Serie Completada 3: Cajeado Circular
**Ejercicios:** O0008, O0009, O0010  
**Material:** Aluminio 4"×2.5"×0.501"  
**Tipo:** Multi-herramienta (4 herramientas por programa)

**Secuencia de operaciones:**
1. **T01** - Broca centros Ø3/8" (centrado previo)
2. **T02** - Broca Ø1/2" (perforado pasante)
3. **T03** - Cortadora Ø1/8" (pocket milling G170/G171)
4. **T04** - Fresa Ø1/2" (contorno multinivel)

**Variaciones:**
- O0008: Modo absoluto G90 (base)
- O0009: Modo incremental G91 en perforado
- O0010: Refinamiento de O0009

**Conceptos nuevos:**
- Workflow completo multi-herramienta
- Cambio entre G90/G91 en mismo programa
- Contorno con múltiples niveles de profundidad

---

### 📐 3. AutoCAD 2D

**Estado:** 🔄 Curso básico en progreso

**Ejercicios básicos:**
- Estrella de 5 puntas (comandos fundamentales)
- Cruz invertida (precisión dimensional)
- Biblioteca de símbolos arquitectónicos
- Plantilla de cajetín profesional

**Proyecto integrador:** Casa Estilo Tradicional 2D
- ✅ Planta arquitectónica completa
- ✅ Planta de techo y fachadas
- ✅ Isométrico y cortes
- ✅ Instalación hidrosanitaria y gas
- ✅ Instalación eléctrica
- ✅ Planos estructurales (cimentación y superestructura)

**Total:** 8 planos técnicos completos

**Comandos dominados:**
- Dibujo: LINE, CIRCLE, ARC, RECTANGLE, POLYGON
- Modificación: TRIM, EXTEND, OFFSET, FILLET, CHAMFER
- Organización: LAYERS, BLOCKS
- En progreso: DIMENSION, HATCH, ARRAY

---

### 🧊 4. SolidWorks 3D

**Estado:** ⏳ Ejercicios iniciales

**Piezas modeladas:**
- Placa (pieza básica con extrusión)
- Tornillo (roscado, revoluciones)
- Práctica 2 (combinación de operaciones)
- Ensamblaje 1 (combinación de piezas)

**Planos generados:**
- 6 PDFs con vistas ortogonales y dimensiones

**Operaciones aprendidas:**
- Extrusión (bosses y cortes)
- Revolución
- Redondeos y chaflanes
- Ensamblajes básicos con restricciones

**Pendiente:**
- Modelado avanzado (barridos, lofts)
- Piezas de chapa metálica
- Simulación de ensamblajes móviles
- Generación de código CNC desde SolidWorks CAM

---

## 🎓 Habilidades en Desarrollo

### Nivel Actual por Área

| Habilidad | Nivel Actual | Progreso | Certificación |
|-----------|--------------|----------|---------------|
| **Torno Convencional** | 🟢 Intermedio | 60% | En curso CECATI |
| **Fresado Manual** | 🟡 Básico | 20% | Planeado |
| **Programación CNC FANUC** | 🟡 Básico-Intermedio | 45% | En curso CECATI |
| **AutoCAD 2D** | 🟡 Básico | 35% | Planeado Autodesk |
| **SolidWorks 3D** | 🟡 Básico | 25% | Planeado CSWA |
| **Lectura de Planos** | 🟢 Intermedio | 55% | En desarrollo |
| **Metrología** | 🟡 Básico | 30% | En curso |

**Leyenda:**
- 🟢 Verde: Competente, puedo trabajar de forma independiente
- 🟡 Amarillo: Aprendiendo, requiero supervisión
- 🔴 Rojo: Principiante absoluto

---

## 📊 Estadísticas del Repositorio

```
Total de archivos:        ~85
Programas CNC (.nc):      10
Planos técnicos:          18+ (PNG, JPG, PDF)
Modelos 3D:               4 (.SLDPRT, .SLDASM)
Archivos CAD:             3 (.dwg)
Documentación:            5 (README, LEARNING, guías)
Recursos (PDF/HTML):      12
```

**Líneas de código G-code escritas:** ~1,200+  
**Simulaciones exitosas:** 10/10 programas

---

## 🛠️ Herramientas y Software

### Software Utilizado

| Software | Versión | Uso Principal |
|----------|---------|---------------|
| **Denford FANUC Milling** | v1.96 | Simulación CNC (fresadora) |
| **AutoCAD** | 2023 | Dibujo técnico 2D |
| **SolidWorks** | 2023 Student | Modelado 3D y ensamblajes |
| **Git + GitHub** | 2.43+ | Control de versiones |
| **VSCode** | Latest | Editor de código G-code |
| **Claude Code** | Latest | Asistente de programación |

### Máquinas y Equipos (CECATI 17)

- Torno convencional Harrison M300 (13" × 40")
- Fresadora CNC Denford (simulador)
- Instrumentos de medición (vernier, micrómetro, comparador)

---

## 📖 Documentación Especial

### 📚 LEARNING.md — Bitácora de Aprendizaje

El archivo más importante del repositorio. Documenta:

- ✅ **Errores cometidos** y por qué ocurrieron
- 🔧 **Soluciones aplicadas** paso a paso
- 💡 **Lecciones aprendidas** de cada ejercicio
- 📈 **Progresión técnica** desde básico a profesional

**Secciones principales:**
1. Fase 1: Primeros pasos con G-code (Cilindros)
2. Fase 2: Interpolación circular - Método R (Letra S)
3. Fase 3: Coordenadas incrementales G91
4. Fase 4: Método I,J - El desafío
5. Fase 5: Velocidades y RPM
6. Errores comunes y soluciones (tabla de 10 errores)
7. Transición hacia mejores prácticas

**[→ Leer LEARNING.md completo](LEARNING.md)**

---

### 📋 Inventario Completo

Documento generado por Cowork con listado exhaustivo de todos los archivos.

**[→ Ver inventario](5.recursos/INVENTARIO_COMPLETO.md)**

---

## 🎯 Objetivos y Próximos Pasos

### ✅ Completado (Febrero 2026)
- [x] Dominar comandos básicos de G-code (G00, G01, G02, G03)
- [x] Comprender ciclos fijos (G81, G83)
- [x] Diferenciar G90 vs G91
- [x] Proyecto AutoCAD completo (8 planos)
- [x] Simulaciones CNC exitosas (3 series, 10 programas)

### 🔄 En Progreso
- [ ] Dominar método I,J para arcos (requiere más práctica)
- [ ] Implementar múltiples pasadas incrementales
- [ ] Acotación profesional en AutoCAD
- [ ] Modelado intermedio en SolidWorks

### 🎯 Próximos 2 Meses
1. **CNC:**
   - 5 ejercicios adicionales con método I,J
   - Introducción a compensación G41/G42
   - Primer uso de subrutinas M98/M99

2. **AutoCAD:**
   - Proyecto arquitectónico original (diseño propio)
   - Dominar DIMENSION y HATCH
   - Presentación profesional con layouts

3. **SolidWorks:**
   - Integrar SolidWorks CAM
   - Generar código CNC desde modelo 3D
   - Comparar código manual vs CAM

4. **Documentación:**
   - Actualizar LEARNING.md con ejercicio cajeado
   - Crear cheatsheet I,J con ejemplos
   - Video tutorial de mi progreso

---

## 🏆 Certificaciones Planeadas

### Corto Plazo (2026)
- 🎯 **Constancia CECATI 17** — Torno y CNC (Mayo 2026)
- 🎯 **Constancia CECATI 17** — AutoCAD Básico (Junio 2026)

### Mediano Plazo (2026-2027)
- 🎯 **Autodesk Certified User** — AutoCAD (2026)
- 🎯 **CSWA** (Certified SolidWorks Associate) (2027)
- 🎯 **CSWP** (Certified SolidWorks Professional) (2027+)

### Largo Plazo (2027+)
- 🎯 **FANUC CNC Programming Certification**
- 🎯 **Mastercam Certified**

---

## 🤝 Contribuciones y Contacto

Este es un repositorio personal de aprendizaje, pero estoy abierto a:

- 💬 Feedback sobre mi código CNC
- 📖 Sugerencias de recursos de aprendizaje
- 🐛 Correcciones en mis programas
- 🤝 Colaboración con otros estudiantes de CECATI

**Institución:** CECATI No. 17 — Centro de Capacitación para el Trabajo Industrial  
**Ubicación:** Querétaro, México  
**Período:** Enero 2026 - Presente

---

## 📜 Licencia

Este repositorio contiene ejercicios educativos y trabajo académico.  
Los planos del profesor son propiedad de CECATI 17.  
Mi código y documentación están disponibles libremente para fines educativos.

---

## 🙏 Agradecimientos

- **Profesor de CNC — CECATI 17:** Por ejercicios estructurados y retroalimentación
- **Claude (Anthropic AI):** Por análisis detallados de código y guías paso a paso
- **Comunidad GitHub:** Por recursos y buenas prácticas de documentación
- **Denford Ltd:** Por el excelente simulador FANUC

---

## 📌 Notas Finales

### Sobre la Naturaleza Didáctica del Código

Los programas CNC en este repositorio son **ejercicios de aprendizaje progresivo**. No todos implementan mejores prácticas profesionales porque el objetivo es:

1. **Primero:** Comprender cada comando G y M individualmente
2. **Segundo:** Practicar sintaxis y lógica de programación
3. **Tercero:** Simular y corregir errores
4. **Cuarto:** Iterar hacia código más profesional

**Ejemplo de evolución:**
- O0004 (primera S): Código funcional básico con errores
- O0005 (S incremental): Dominio de G91
- O0006 (S con I,J): Primer intento método profesional (con errores documentados)
- Próximo: O0011+ con código optimizado

Esta progresión está **intencionalmente documentada** en LEARNING.md.

---

### Control de Versiones

**Commits atómicos:** Cada cambio significativo tiene su propio commit descriptivo.  
**Historial limpio:** Fácil de navegar y entender la evolución del aprendizaje.  
**Mensajes descriptivos:** Formato `tipo: descripción` (feat, docs, assets, chore).

**Ejemplo de historial reciente:**
```
● feat: agrega programas ejercicio cajeado circular (O0008-O0010)
● assets: agrega simulaciones ejercicio cajeado circular
● docs: agrega plano ejercicio cajeado circular
● docs: actualiza README de 2.CNC y agrega bitácora de aprendizaje
● feat: agrega ejercicios CNC O0003 (cilindros) y O0004 (letra S base)
```

---

**Última actualización:** 17 de Febrero 2026  
**Próxima revisión:** Después de completar ejercicios con I,J y proyecto AutoCAD original

---

*"El código perfecto es el resultado de múltiples refinamientos, no del primer intento."*  
— Lección aprendida en LEARNING.md
