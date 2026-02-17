# INVENTARIO COMPLETO DEL REPOSITORIO MAQUINADO
**Generado:** 17 de febrero de 2026
**Total de archivos:** 74

---

## 📁 ESTRUCTURA GENERAL

```
maquinado/
├── 1.Torno-Fresado/
│   ├── Foto_planos/ (5 imágenes JPEG)
│   ├── planos/ (5 imágenes PNG)
│   └── practicas/ (vacío)
├── 2.CNC/
│   ├── ejercicios-letra-S/
│   │   ├── O0005_S_Incremental_G91_R.nc
│   │   ├── O0006_S_Absoluto_IJ_375.nc
│   │   ├── O0007_S_Incremental_IJ_375.nc
│   │   ├── referencia/ (1 imagen PNG)
│   │   └── simulaciones/ (2 imágenes PNG)
│   ├── codigos-g/ (vacío)
│   ├── planos/ (3 imágenes PNG + carpeta Fotos_planos con 3 imágenes)
│   ├── recursos/
│   │   ├── G_code_Fanuc.html
│   │   ├── Guía_Rápida_Código_G.pdf
│   │   └── Manual/ (9 imágenes JPEG)
│   ├── simulador-denforf-fanuc/ (vacío)
│   └── README.md
├── 3.autocad/
│   ├── 8 imágenes JPEG (planos arquitectónicos)
│   ├── ejercicios/ (vacío)
│   ├── proyectos/ (vacío)
│   ├── 3 archivos DWG
│   └── 3 archivos PDF
├── 4.solidworks/
│   ├── ejercicios/ (4 archivos: 1 ensamblaje, 3 piezas)
│   ├── modelos-3d/ (vacío)
│   └── planos/ (6 archivos PDF)
├── 5.recursos/
│   ├── apuntes/ (vacío)
│   ├── GUÍA_PROFESIONAL_DE_TORNO.pdf
│   ├── La_Pirámide_de_la_Maestría_del_Torno.pdf
│   └── tsabla_conversion.png
└── Archivos raíz (ver detalles abajo)
```

---

## 📄 CONTENIDO DE ARCHIVOS DE TEXTO

### 1. README.md (Raíz)
```markdown
# Maquinado - CECATI 17

Repositorio personal de ejercicios y prácticas de maquinado, diseño CAD y programación CNC.

## 📚 Contenido

Este repositorio contiene el trabajo desarrollado durante mi formación en:

- **Torno Convencional**: Prácticas y planos de piezas maquinadas
- **CNC (Simulador Denforf Fanuc)**: Programación y simulación de piezas
- **AutoCAD**: Ejercicios de dibujo técnico 2D desde cero
- **SolidWorks**: Modelado 3D y diseño de piezas desde cero

## 🎓 Institución

**CECATI No. 17**
Centro de Capacitación para el Trabajo Industrial

## 📂 Estructura del Repositorio
```
maquinado/
├── torno/              # Prácticas de torno convencional
├── cnc/                # Programación CNC y simulaciones
├── autocad/            # Ejercicios de AutoCAD
├── solidworks/         # Modelos 3D y proyectos
└── recursos/           # Apuntes y material de apoyo
```

## 🛠️ Herramientas

- **Torno**: Convencional
- **CNC**: Simulador Denforf Fanuc
- **CAD**: AutoCAD
- **CAM/CAD**: SolidWorks

## 📝 Progreso

### Torno
- [x] Práctica 1 - Flecha (CECATI No.17)
- [x] Práctica 2 - Flecha roscada
- [ ] En progreso...

### CNC
- [x] Control numérico básico
- [x] Ejercicio bloque con cilindros
- [ ] En progreso...

### AutoCAD
- [ ] Curso básico desde cero en progreso

### SolidWorks
- [ ] Curso básico desde cero en progreso

## 📈 Habilidades en Desarrollo

| Habilidad | Nivel | Certificación |
|-----------|-------|---------------|
| Torno | 🟢 Intermedio | En curso |
| CNC Fanuc | 🟡 Básico | En curso |
| AutoCAD | 🟡 Básico | Planeado |
| SolidWorks | 🟡 Básico | Planeado |

## 📌 Notas

Este repositorio se actualiza constantemente conforme avanzo en mis cursos y prácticas.

---

*Última actualización: Febrero 2026*
```

### 2. 2.CNC/README.md
**Contenido:** (Archivo casi vacío, solo 1 línea)

---

## 💾 ARCHIVOS DE CÓDIGO G-CODE (CNC)

### 3. O0005_S_Incremental_G91_R.nc
**Descripción:** Programa CNC para mecanizar letra "S" en modo incremental (G91)
**Herramienta:** Fresa D.5
**Material:** Billet 3"x5"x0.75"

```gcode
[BILLET X3 Y5 Z.75
[TOOLDEF T01 D.5
O0005
(LETRA S - MODO INCREMENTAL G91)
N10 G20 G80 G54 G90
N15 G00 X-0.5 Y1.5
N20 G00 Z1
N25 G01 Z-.25 F100
N30 G01 X0
N35 G91
N40 G03 X1.5 Y-1.5 R1.5
N45 G03 X1.5 Y1.5 R1.5
N50 G03 X-1.5 Y1.5 R1.5
N55 G02 X-.5 Y.5 R.75
N60 G02 X.5 Y.5
N65 G02 X.5 Y-.5
N70 G01 X-.5
N75 G01 X.5
N80 G01 Y-.5
N85 G01 X1
N90 G01 Y.5
N95 G03 X-1.5 Y1.5 R1.5
N100 G03 X-1.5 Y-1.5 R1.5
N105 G03 X1.5 Y-1.5 R1.5
N110 G02 X.5 Y-.5 R.75
N115 G02 X-.5 Y-.5 R.75
N120 G02 X-.5 Y.5 R.75
N125 G01 X.5
N130 G01 X-.5
N135 G01 Y.5
N140 G01 X-1
N145 G01 Y3
N150 G01 X3
N155 G01 Y-4.99
N160 G01 X-3
N165 G01 Y2
```

### 4. O0006_S_Absoluto_IJ_375.nc
**Descripción:** Programa CNC para mecanizar letra "S" en modo absoluto con notación IJ
**Herramienta:** Cortadora D.375
**Material:** Billet 3"x5"x0.75"

```gcode
[BILLET X3 Y5 Z.75
[TOOLDEF T01 D.375
O0006
(CORTADORA .375)
N10 G20 G80 G54 G90
N15 G00 X-.5 Y1.5
N30 G00 Z1
N35 G01 Z-.25 F80
N40 G01 X0
N45 G03 X1.5 Y0 I1.5 J0
N50 G03 X1.5 Y3 I0 J1.5
N55 G02 X1 Y3.5 I0 J.5
N60 G02 X2 Y3.5 I.5 J0
N65 G01 X1.5 Y3.7
N70 G01 X1.2 Y3.4
N75 G01 X2 Y3.4
N80 G01 Y3.3
N85 G01 X3
N90 G01 Y3.5
N95 G03 X1.5 Y5 I-1.5 J0
N100 G03 X1.5 Y2 I0 J-1.5
N105 G02 X1.5 Y1 I0 J-.5
N110 G02 X1 Y1.5 I0 J.5
N115 G01 X1.7 Y1.3
N120 G01 X1.75 Y1.7
N125 G01 X0
N125 G01 Y0
N130 G01 X3
N135 G01 Y3
N140 G01 X1.75
N145 G01
```

### 5. O0007_S_Incremental_IJ_375.nc
**Descripción:** Programa CNC para mecanizar letra "S" en modo incremental con notación IJ
**Herramienta:** Cortadora D.375
**Material:** Billet 3"x5"x0.75"

```gcode
[BILLET X3 Y5 Z.75
[TOOLDEF T01 D.375
O0007
(CORTADORA .375)
N10 G20 G80 G54 G90
N30 G00 Z1
N40 G01 X-2 Y-2
N45 G01 Z-.25 F80
N45 G03 X1 Y-2 R1.5
N55 G03 X-.5 Y-.5 R1.5
N60 G01 X-1 Y0
N65 G02 R.5
N70 G01 X-.8
N75 G02 R.25
N80 G01 X0 Y0
N85 G01 Y-.5
N90 G01 X1
N95 G01 Y0
N100 G03 X-.5 Y1.5 R1.5
N105 G03 X-2 Y0 I0 J-1.5
N110 G03 X-.5 Y-1.5 R1.5
N115 G02 X0 Y-2 I0 J-.5
N120 G02 X-1 Y-2 R.5
N125 G01 X-.2
N130 G03 R.25
N135 G01 X-1
N140 G01 Y-1.5
N145 G01 X-2
N150 G01 Y-3.5
N155 G01 X1
N160 G01 Y1.5
N165 G01 X-2
N170 G01 Y-2
```

### 6. FRESA3.nc.txt / FRESA3.txt
**Descripción:** Programa CNC para mecanizar patrón de cilindros (matriz 5x2)
**Herramientas:**
- T01: Broca de centros D5mm
- T02: Broca D10mm
- T03: Cortadora D9.5mm
**Material:** Billet 120x80x25mm

```gcode
[BILLET X120 Y80 Z25
[TOOLDEF T01 D5
[TOOLDEF T02 D10
[TOOLDEF T03 D9.5
O0003
(FRESA3)
N10 G21 G90 G54 G40
N15 G90 G95 G17 G80

(BROCA DE CENTROS)
N20 M06 T01
N25 M03 S2000
N30 G00 X20 Y15
N35 G00 Z1
N40 G01 Z-5 F100
N45 G00 Z1
N50 G00 X40
N55 G01 Z-5
N60 G00 Z1
... (continúa con patrón de centros 5x2)

(BROCA DE 10MM)
N175 M06 T02
N180 M03 S1000
N185 G00 X00 Y15
N186 G00 Z1
N187 G91 G73 X20 Z-22 R2 Q5 K5 F80
... (ciclos de perforación)

(CORTADORA 9.5MM)
N210 M06 T03
N215 S1000
N220 G00 X20 Y15
N225 G00 Z1
N226 G01 Z0
N230 G170 R0 P0 Q1 X20 Y15 Z-10 I1 J1 K10
N235 G171 P12 S2000 R16 F12 B2500 J15
... (fresado de cilindros)

N350 M30 M05
```

### 7. FRESA4.txt
**Descripción:** Programa CNC para mecanizar letra "S" (versión anterior)
**Herramienta:** Cortadora D.5
**Material:** Billet 3"x5"x0.75"

```gcode
[BILLET X3 Y5.Z.75
[TOOLDEF T01 D.5
O0004
(CORTADORA .5)
N10
N15
N20 G20 G80 G54 G90
N25 G28 G40 G95
N30 M06 T01
N35 G00 X-.5 Y1.5
N40 G00 Z.1
N45 G01 Z-.250 F100
N50 G01 X0
N55 G03 X1.5 Y0 R1.5
N60 G03 X3 Y1.5 R1.5
N65 G03 X1.5 Y3 R1.5
N70 G02 X1 Y3.5 R.75
N75 G02 X1.5 Y4 R.75
N80 G02 X2 Y3.5 R.75
N81 G01 X1
N83 G01 X2
N87 G01 Y3
N88 G01 X3
N89 G01 Y3.5
N90 G03 X1.5 Y5 R1.5
N95 G03 X0 Y3.5 R1.5
N100 G03 X1.5 Y2 R1.5
N105 G02 X2 Y1.5 R.75
N110 G02 X1.5 Y1 R.75
N115 G02 X1 Y1.5 R.75
N120 G01 Y2
N121 G01 X1.5 Y1.5 R1.5
N125 G01 Y2
N130 G01 X0
N135 G01 Y0
N140 G01 X3
N148 G01 Y5
N149 G01 X0
N150 G01 Y0
N151 G28 Z0
N155 M30 M05
```

---

## 🌐 ARCHIVO HTML

### 8. 2.CNC/recursos/G_code_Fanuc.html
**Descripción:** Guía visual interactiva de código G (Fanuc/Denford)
**Tipo:** Cheat sheet con Tailwind CSS
**Contenido:** Tablas organizadas por categorías:
- Comandos de Movimiento (G00-G03)
- Sistemas de Coordenadas (G17-G91)
- Compensación de Herramienta (G40-G49)
- Ciclos Fijos (G80-G99)
- Códigos M (máquina)

---

## 📚 GUÍA PROFESIONAL DE TORNO

### 9. # GUÍA PROFESIONAL DE TORNO (De principi.md
**Descripción:** Guía completa de operación de torno (33,417 bytes)
**Secciones principales:**

1. Introducción al torno
2. Seguridad industrial
3. Partes del torno
4. Montaje y sujeción
5. Herramientas de corte
6. Operaciones básicas
7. Control dimensional
8. Parámetros de corte
9. Acabado superficial
10. Troubleshooting

**Extracto:** (Ver primeras 100 líneas mostradas arriba)

---

## 🖼️ ARCHIVOS DE IMÁGENES (36 archivos)

### 1.Torno-Fresado/
**Foto_planos/** (5 imágenes JPEG):
- Base_lampara.jpeg
- Destapador.jpeg
- Exentrico.jpeg
- Flecha1.jpeg
- Flecha2.jpeg

**planos/** (5 imágenes PNG):
- Destapador.png
- Exentrico.png
- Flecha1.png
- Flecha2.1.png
- Flecha2.png

### 2.CNC/
**ejercicios-letra-S/referencia/**
- LetraS_resultado_mecanizado.png (resultado final de la letra S)

**ejercicios-letra-S/simulaciones/**
- FRESA56_simulacion_2D.png
- FRESA56_simulacion_3D.png

**planos/**
- 1.0(Enero).png
- 2.0(Enero).png
- 3.0(Febrero).png

**planos/Fotos_planos/**
- 1.0 (Enero).png
- 2.0 (Enero).png
- 3.0 (febrero).png

**recursos/Manual/** (9 imágenes JPEG de WhatsApp)
- WhatsApp Image 2026-02-12 at 9.15.07 AM (1-3).jpeg
- WhatsApp Image 2026-02-12 at 9.15.07 AM.jpeg
- WhatsApp Image 2026-02-12 at 9.15.08 AM (1-3).jpeg
- WhatsApp Image 2026-02-12 at 9.15.08 AM.jpeg
- WhatsApp Image 2026-02-12 at 9.36.35 AM.jpeg

### 3.autocad/ (8 imágenes JPEG)
- 1.- Casa Estilo Tradicional 2D 1.jpg.jpeg
- 2.- Planta Arquitectónica 2D.jpg.jpeg
- 3.- Planta Techo y Fachada 2D.jpg.jpeg
- 4.- Isométrico y Corte Longitudinal 2D.jpg.jpeg
- 5.- Instalación Hidrosanitario y Gas 2D.jpg.jpeg
- 6.- Instalación Electríca 2D.jpg.jpeg
- 7.- Plano Estructural 1 2D.jpg.jpeg
- 8.- Plano Estructural 2 2D.jpg.jpeg

### 5.recursos/
- tsabla_conversion.png (tabla de conversión de unidades)

### Raíz del repositorio:
- 20260131_2319_Image Generation_remix_01kgbt629sfe98eywc9kw5t5t1.png
- Chearsheet-programacion-CNC-Denford-Fanuc(2).png
- Cheatsheet-programacion-CNC-Denford-Fanuc.png
- Guia-rapida-programacion-CNC.png
- Guía-Rapida-CNC-Torno-Fresa.png

---

## 📑 ARCHIVOS PDF (9 archivos)

### 3.autocad/
- **Dibujo 1.- Estrella.pdf** - Ejercicio de dibujo técnico
- **La Armonía en el Color - Nuevas Tendencias.pdf** - Teoría del color
- **Sensación+-+Significado+y+aplicación+del+color+FINAL.pdf** - Teoría del color aplicada

### 4.solidworks/planos/ (6 archivos)
- Dibujo 1, Caja.pdf
- Dibujo 1, Práctica.pdf
- Dibujo 2, Lápiz.pdf
- Dibujo 2, Práctica.pdf
- Dibujo 3, Práctica.pdf
- Dibujo 4, Práctica.pdf

### 5.recursos/
- **GUÍA_PROFESIONAL_DE_TORNO.pdf** - Guía completa de torno
- **La_Pirámide_de_la_Maestría_del_Torno.pdf** - Metodología de aprendizaje

### 2.CNC/recursos/
- **Guía_Rápida_Código_G.pdf** - Referencia rápida de código G

### Raíz del repositorio:
- **CNC_Programming_Reference_Guide.pdf** - Guía de programación CNC
- **harrison-m300-lathe-operations-and-parts-manual-12-speed-gear-head-13-x-40-28525hlnkrf.pdf** - Manual del torno Harrison M300

---

## 🔧 ARCHIVOS DE DISEÑO

### AutoCAD (.dwg) - 3 archivos
**Ubicación:** 3.autocad/
- **Dibujo 2.- Cruz Invertida.dwg** - Ejercicio de dibujo
- **Libreria.dwg** - Biblioteca de símbolos
- **Pie de Plano.dwg** - Plantilla para cajetín

### SolidWorks - 4 archivos
**Ubicación:** 4.solidworks/ejercicios/

**Ensamblajes (.SLDASM):**
- Ensamblaje1.SLDASM

**Piezas (.SLDPRT):**
- Placa.SLDPRT
- Practica_2.SLDPRT
- Tornillo.SLDPRT

---

## 📄 OTROS ARCHIVOS

### Documentos Word
- **CNC_Denford_Fanuc_Cheatsheet.docx** (raíz) - Cheat sheet de CNC en formato Word

### Archivos de control
- **desktop.ini** (raíz) - Configuración de carpeta de Windows (no existe o está vacío)

---

## 📊 ESTADÍSTICAS DEL REPOSITORIO

| Categoría | Cantidad |
|-----------|----------|
| **Archivos de código G (.nc, .txt)** | 7 |
| **Imágenes (PNG, JPEG)** | 36 |
| **Documentos PDF** | 11 |
| **Archivos CAD (DWG)** | 3 |
| **Archivos SolidWorks (SLDPRT, SLDASM)** | 4 |
| **Archivos HTML** | 1 |
| **Archivos Markdown (.md)** | 3 |
| **Archivos Word (DOCX)** | 1 |
| **Carpetas vacías** | 8 |
| **TOTAL DE ARCHIVOS** | **74** |

---

## 🔍 CARPETAS VACÍAS (Listas para contenido futuro)

1. `1.Torno-Fresado/practicas/`
2. `2.CNC/codigos-g/`
3. `2.CNC/simulador-denforf-fanuc/`
4. `3.autocad/ejercicios/`
5. `3.autocad/proyectos/`
6. `4.solidworks/modelos-3d/`
7. `5.recursos/apuntes/`
8. `2.CNC/ejercicios-letra-S/planos/`

---

## 📝 NOTAS ADICIONALES

### Organización reciente
- Se creó recientemente la estructura `2.CNC/ejercicios-letra-S/` para organizar los ejercicios de la letra S
- Se renombraron archivos FRESA5-7.txt a nombres descriptivos con extensión .nc
- Se movieron imágenes relacionadas a carpetas de referencia y simulaciones

### Estado del repositorio
- **Activo:** Febrero 2026 (CECATI No. 17)
- **Git:** Repositorio versionado con `.git/`
- **Enfoque:** Aprendizaje práctico de manufactura y diseño CAD/CAM

### Áreas de conocimiento cubiertas
1. ✅ Torno convencional (prácticas y planos)
2. ✅ CNC Fanuc (programación G-code)
3. ✅ AutoCAD 2D (planos arquitectónicos)
4. ✅ SolidWorks (modelado 3D básico)
5. ✅ Seguridad industrial
6. ✅ Teoría del color (para diseño)

---

**FIN DEL INVENTARIO**
