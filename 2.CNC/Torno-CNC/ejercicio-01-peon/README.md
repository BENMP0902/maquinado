# Práctica 1: Esquivel - Torno CNC

## 📐 Descripción de la Pieza

**Nombre:** Esquivel (Heicoil / Inserto)  
**Máquina:** Torno CNC Denford FANUC v1.42  
**Material:** Acero 1010/1020  
**Diámetro inicial:** Ø33 mm  
**Longitud:** 65 mm

## 🔧 Herramientas Utilizadas

| Herramienta | Código | Operación | RPM |
|---|---|---|---|
| **T00** | Roughing 1 | Desbaste cabeza | 1200 |
| **T02** | Roughing 2 | Desbaste general | - |
| **T07** | Finishing | Acabado (semi-acabado) | - |
| **T03** | Parting | Corte/separación | - |

## 📊 Secuencia de Operaciones

### 1. CABEZA (N010-N235)
- Desbaste de la cabeza hexagonal
- Múltiples pasadas desde Ø32→Ø22
- Profundidad progresiva hasta Z-55
- Herramienta: T00

### 2. CAMBIO DE HERRAMIENTA (N236-N275)
- Transición a herramienta T02
- Desbaste de cavidades internas
- Coordenadas X19-X21 y Z-14 a Z-27

### 3. ACABADO (N290-N345)
- Herramienta: T07 (Finishing)
- Operación de semi-acabado
- Transiciones suaves (X17→X21, Z-2→Z-50)

### 4. CORTADOR (N500-N510)
- Herramienta: T03 (Parting)
- Corte final a Z-53

## ⚙️ Parámetros Principales

- **Sistema métrico:** G21
- **Velocidad de avance:** F100-F150 (mm/min)
- **Coordenadas:** Absolutas (G90)
- **Home:** G28 U0 W0 (retorno automático)

## 🎯 Notas Pedagógicas

Este programa demuestra:
✅ Manejo secuencial de múltiples herramientas  
✅ Desbaste progresivo con pasadas calculadas  
✅ Transiciones suaves entre operaciones  
✅ Uso de retorno a home (G28) para seguridad  

## 🔍 Análisis del Código

**Línea crítica:** N236 (Cambio herramienta)
```
N236 G28 U0 W0      ; Retorno a home
(CAMBIO DE HERRAMIENTA)
N237 M06 T02        ; Seleccionar herramienta T02
```

**Patrón de desbaste (N100-N235):**
```
G00 XN Z1           ; Aproximación rápida
G01 XN Z-prof F100  ; Corte lineal
G00 XN Z1           ; Retracción
```

## ✅ Verificación

- [x] Código simulado en Denford FANUC v1.42
- [x] Trayectorias sin colisiones
- [x] Herramientas correctas (T00, T02, T07, T03)
- [x] Retornos a home después de cambios

---

**Fecha:** Marzo 2026  
**Simulador:** Denford FANUC Turning v1.42  
**Estado:** Listo para máquina real (bajo supervisión)