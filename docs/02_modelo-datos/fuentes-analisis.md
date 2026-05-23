# Fuentes de datos para análisis

## Objetivo

Documentar las fuentes de datos disponibles para análisis gerencial en Stylos OS, su contenido, frecuencia, nivel de confiabilidad y limitaciones. Este documento es la base para responder consultas libres sin crear scripts ni automatizaciones.

---

## Fuentes disponibles

### Google Sheets — Caja_diaria

| Atributo | Detalle |
|----------|---------|
| **Fuente** | Google Sheets — `Stylos_Data` |
| **Qué aporta** | Ingresos diarios desglosados por medio de pago (Efectivo, MPD, MPM, Tarjetas) y total por jornada |
| **Frecuencia esperada** | Diaria |
| **Nivel de confiabilidad** | Alto — Datos cargados manualmente con validación informal (cierre de caja) |
| **Limitaciones** | No tiene granularidad horaria; no distingue entre servicios individuales; no identifica cliente |
| **Estado** | Disponible |
| **Referencia** | `../02_modelo-datos/diccionario-datos.md` (sección Caja diaria) |

---

### Google Sheets — Egresos

| Atributo | Detalle |
|----------|---------|
| **Fuente** | Google Sheets — `Stylos_Data` |
| **Qué aporta** | Gastos detallados del local con categoría, subcategoría, persona responsable y medio de pago |
| **Frecuencia esperada** | Diaria / Semanal |
| **Nivel de confiabilidad** | Medio — PersonaID frecuentemente vacío; sin validación visible contra diccionarios |
| **Limitaciones** | Atribución de gastos a personas incompleta; texto libre en Detalle genera inconsistencia; CategoriaID/SubCategoriaID sin validación visible |
| **Estado** | Disponible |
| **Referencia** | `../02_modelo-datos/diccionario-datos.md` (sección Egresos) |

---

### Google Sheets — Comisiones

| Atributo | Detalle |
|----------|---------|
| **Fuente** | Google Sheets — `Stylos_Data` |
| **Qué aporta** | Comisiones diarias por barbero, con desglose de servicios, productos y formas de cobro |
| **Frecuencia esperada** | Diaria |
| **Nivel de confiabilidad** | Medio — PersonaID y ComisionID vacíos en registros tempranos; fórmulas no documentadas |
| **Limitaciones** | PersonaID=7 con Servicios=0 tiene interpretación especial (licencia médica); faltan fórmulas documentadas de Total_Ventas y Total_Abonado |
| **Estado** | Disponible |
| **Referencia** | `../02_modelo-datos/diccionario-datos.md` (sección Comisiones) |

---

### Google Sheets — Cuota parte

| Atributo | Detalle |
|----------|---------|
| **Fuente** | Google Sheets — `Stylos_Data` o `Stylos_Analisis` (pendiente confirmar) |
| **Qué aporta** | Distribución de ingresos por cuota parte entre los miembros del equipo |
| **Frecuencia esperada** | Mensual |
| **Nivel de confiabilidad** | Pendiente de relevar |
| **Limitaciones** | Hoja no verificada contra planilla real; fórmulas no documentadas |
| **Estado** | Parcial — Pendiente de relevar columnas y fórmula |
| **Referencia** | `../02_modelo-datos/diccionario-datos.md` (sección Cuota parte = TODO) |

---

### Google Sheets — Presupuesto

| Atributo | Detalle |
|----------|---------|
| **Fuente** | Google Sheets — `Stylos_Presupuesto` (pendiente confirmar) |
| **Qué aporta** | Presupuesto mensual/anual con ejecución y desvíos |
| **Frecuencia esperada** | Mensual |
| **Nivel de confiabilidad** | Pendiente de relevar |
| **Limitaciones** | Hoja no verificada; archivo no confirmado; fórmulas no documentadas |
| **Estado** | Parcial — Pendiente de confirmar archivo y contenido |
| **Referencia** | `../02_modelo-datos/diccionario-datos.md` (sección Presupuesto = TODO) |

---

### Google Sheets — Dashboard

| Atributo | Detalle |
|----------|---------|
| **Fuente** | Google Sheets — `Stylos_Analisis` (pendiente confirmar) |
| **Qué aporta** | Indicadores clave de salud del negocio en formato resumen |
| **Frecuencia esperada** | Bajo demanda |
| **Nivel de confiabilidad** | Pendiente de relevar |
| **Limitaciones** | Hoja no verificada contra planilla real; contenido y fórmulas no documentados |
| **Estado** | Parcial — Pendiente de relevar columnas y fuentes |
| **Referencia** | `../02_modelo-datos/diccionario-datos.md` (sección Dashboard = TODO) |

---

### Fresha — Reporte de ventas (export CSV)

| Atributo | Detalle |
|----------|---------|
| **Fuente** | Fresha — `report_sales-log-detail` exportado manualmente |
| **Qué aporta** | Detalle de cada venta: fecha/hora, tipo, artículo, categoría, cliente, miembro del equipo, canal, ventas brutas, descuentos, ventas netas, total |
| **Frecuencia esperada** | Manual — Se exporta cuando se necesita analizar |
| **Nivel de confiabilidad** | Alto — Datos de plataforma de reservas; no modificado manualmente |
| **Limitaciones** | Export manual requerido; no hay conexión automática; cambios de formato de fecha/hora posibles entre exportaciones |
| **Estado** | Disponible (parcial: formato de fecha/hora requiere validación) |
| **Referencia** | `../02_modelo-datos/mapeo-fresha-sheets.md` |

---

### Cuaderno físico / Hoja diaria

| Atributo | Detalle |
|----------|---------|
| **Fuente** | Registro operativo en papel o PDF |
| **Qué aporta** | Detalle por jornada: servicios, egresos, comisiones, retiros, con medios de pago |
| **Frecuencia esperada** | Diaria |
| **Nivel de confiabilidad** | Medio — Depende de quién registre; formato libre con riesgo de ambigüedad |
| **Limitaciones** | Sin validación automática; abreviaturas pueden ser ambiguas; no hay respaldo digital estructurado |
| **Estado** | Disponible |
| **Referencia** | `../03_procesos/cierre-diario.md`, `../05_templates/registro-diario-fisico.md` |

---

### Google Sheets — Hojas diccionario

| Hoja | Contenido | Estado |
|------|-----------|--------|
| Personas | Nombres y IDs de barberos y participantes del negocio | Parcial — Pendiente de relevar |
| Categorías | Lista de categorías de ingresos/egresos | Parcial — Pendiente de relevar |
| Subcategorías | Detalle por categoría (jerarquía) | Parcial — Pendiente de relevar |
| Medios de pago | Lista de medios de pago aceptados | Parcial — Pendiente de relevar |

---

### Google Sheets — Hojas de memoria

| Hoja | Contenido | Estado |
|------|-----------|--------|
| Eventos | Registro de eventos relevantes del negocio | Parcial — Pendiente de relevar contenido |
| Decisiones | Decisiones tomadas con contexto y resultado | Parcial — Pendiente de confirmar estructura |
| Consultas IA | Preguntas y respuestas con IA | Parcial — Pendiente de confirmar estructura |
| Aprendizajes | Lecciones aprendidas validadas | Parcial — Pendiente de confirmar estructura |

---

## Resumen de estado por fuente

| Fuente | Estado | Nivel de confiabilidad |
|--------|--------|----------------------|
| Caja_diaria | **Disponible** | Alto |
| Egresos | **Disponible** | Medio |
| Comisiones | **Disponible** | Medio |
| Cuota parte | **Parcial** | Por relevar |
| Presupuesto | **Parcial** | Por relevar |
| Dashboard | **Parcial** | Por relevar |
| Fresha (CSV) | **Disponible** | Alto |
| Hoja diaria | **Disponible** | Medio |
| Personas | **Parcial** | Por relevar |
| Categorías | **Parcial** | Por relevar |
| Subcategorías | **Parcial** | Por relevar |
| Medios de pago | **Parcial** | Por relevar |
| Eventos | **Parcial** | Por relevar |
| Decisiones | **Parcial** | Por relevar |
| Consultas IA | **Parcial** | Por relevar |
| Aprendizajes | **Parcial** | Por relevar |

---

## Qué NO son estas fuentes

- **No son una base de datos SQL.** Son hojas de cálculo y exports manuales.
- **No están automatizadas.** Toda exportación requiere intervención manual.
- **No son perfectas.** Tienen gaps de completitud, inconsistencias de formato y campos vacíos.
- **No se modifican desde aquí.** La corrección de datos se hace manualmente en Sheets o en la plataforma de origen.

---

## Referencias

- Modelo de datos: `../02_modelo-datos/estructura-sheets.md`
- Diccionario de datos: `../02_modelo-datos/diccionario-datos.md`
- Plan de validaciones: `../02_modelo-datos/plan-validaciones-sheets.md`
- Mapeo Fresha vs Sheets: `../02_modelo-datos/mapeo-fresha-sheets.md`
- Cruza de datos: `../03_procesos/cruza-datos-inicial.md`