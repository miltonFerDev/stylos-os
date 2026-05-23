# Cruza de datos — Análisis cruzado manual

## Objetivo

Documentar el proceso manual de análisis cruzado entre Google Sheets y Fresha para responder consultas gerenciales. Este documento no implementa scripts ni automatizaciones. Solo describe cómo un analista (o IA assisting) puede cruzar datos hoy, qué cruces tienen prioridad, y qué queda para después.

---

## Principios

1. **El análisis es manual.** Se exportan datos, se comparan visualmente o con ayuda de una IA, se registran hallazgos. No hay pipelines automatizados.
2. **Las diferencias se documentan, no se ocultan.** Si Fresha y Sheets no coinciden, se marca como discrepancia y se propone investigarla.
3. **El nivel de confianza se expresa siempre.** Cada hallazgo lleva su nivel (confirmado, probable, estimado).
4. **No se fuerza el cruce.** Si los datos no permiten una conclusión sólida, se dice "no disponible" y se explica por qué.

---

## Fuentes y su rol en el análisis cruzado

| Fuente | Rol en el análisis |
|--------|-------------------|
| **Caja_diaria** | Consolidado de ingresos por día y medio de pago. Referencia para totales diarios. |
| **Comisiones** | Actividad por barbero. Referencia para validar Fresha por persona. |
| **Egresos** | Gastos del local. Referencia para resultado operativo y anomalías de caja. |
| **Fresha (CSV)** | Detalle de servicios por cliente, barbero, hora y canal. Referencia para actividad y tendencia. |
| **Hoja diaria** | Respaldo operativo del día. Útil cuando hay diferencias entre Fresha y Sheets. |

---

## Flujo de análisis cruzado (manual)

### Paso 1: Definir el objetivo de la consulta

Toda cruza responde a una consulta. El objetivo es claro: qué se quiere saber y por qué surge ahora.

### Paso 2: Identificar las fuentes necesarias

Dependiendo de la consulta, se necesita una o más fuentes:

| Consulta | Fuentes necesarias |
|----------|-------------------|
| ¿Cuánto vendimos este mes? | Caja_diaria (totales), Fresha (detalle por servicio) |
| ¿Los barbijos están activos? | Comisiones (servicios por persona), Fresha (actividad por barbero) |
| ¿Hay gastos fuera de lo normal? | Egresos (por categoría), Caja_diaria (resultado diario) |
| ¿Laclientela está creciendo? | Fresha (clientes nuevos vs recurrentes), Comisiones (tendencia) |
| ¿El sponsor está generando valor? | Egresos (gastos con sponsor), Fresha (canal = sponsor?), Caja_diaria (ingresos en períodos) |

### Paso 3: Exportar los datos necesarios

**Para Sheets:**

1. Ir al archivo correspondiente en Google Sheets.
2. Exportar o copiar los datos relevantes (rango de fechas, columnas necesarias).
3. Usar los CSV de muestra en `data/raw/samples/` como referencia si no se tiene acceso directo ahora.

**Para Fresha:**

1. Ir a Fresha → Reportes → `report_sales-log-detail`.
2. Seleccionar rango de fechas.
3. Exportar a CSV.
4. Guardar en `data/raw/` con nombre que incluya fecha de exportación y rango.

### Paso 4: Resumir los datos

Antes de cruzar, resumir cada fuente por sí sola:

| Fuente | Resumen esperado |
|--------|-----------------|
| Caja_diaria | Total por día, total por medio de pago, total por período |
| Comisiones | Servicios por persona, comisiones totales por persona, días activos |
| Egresos | Total por categoría, total por período, gastos fuera de patrón |
| Fresha | Servicios por día, clientes únicos, barberos activos, canal, tendencia |

### Paso 5: Comparar y cruzar

Comparar los resúmenes entre fuentes buscando:

- **Coincidencias**: ¿Los totales de Fresha coinciden con Caja_diaria? ¿Los servicios en Fresha coinciden con Comisiones?
- **Discrepancias**: ¿Hay días donde Fresha tiene actividad pero Sheets no? ¿Hay comisiones en Sheets sin对应 en Fresha?
- **Patrones**: ¿La actividad de cierto barbero sube o baja? ¿Los gastos de cierta categoría crecen?
- **Señales tempranas**: ¿Hay algo que todavía no es un problema pero podría serlo?

### Paso 6: Documentar hallazgos

Por cada hallazgo:

1. Qué se observó (hecho).
2. De qué fuente(s) viene.
3. Qué nivel de confianza tiene.
4. Qué implica para el negocio.
5. Si requiere acción o solo monitoreo.

---

## Cruces con prioridad hoy

Estos cruces se pueden hacer con los datos disponibles actualmente, aunque siempre con cautela y marcando limitaciones.

### Cruce A: Ingresos diarios Fresha vs Caja_diaria

| Aspecto | Detalle |
|---------|---------|
| **Qué cruza** | Suma de Total en Fresha por día vs Total Barbería en Caja_diaria |
| **Validación** | Día a día, comparando totales |
| **Nivel de confianza del cruce** | Probable — Los totales deberían coincidir, pero puede haber diferencias por timing de carga |
| **Discrepancia aceptable** | Pequeña diferencia (<5%) puede ser timing. Diferencia mayor requiere investigación. |
| **Si no coinciden** | Documentar la diferencia. No forzar explicación. Investigar原因: ¿carga tardía? ¿diferencia de fecha? ¿dato faltante? |

### Cruce B: Actividad de barbero en Fresha vs Comisiones

| Aspecto | Detalle |
|---------|---------|
| **Qué cruza** | Servicios por "Miembro del equipo" en Fresha vs PersonaID + Servicios en Comisiones |
| **Validación** | Por persona y por día |
| **Nivel de confianza del cruce** | Parcial — La relación es por nombre, no por ID. Puede haber inconsistencias de spelling. |
| **Si no coinciden** | Verificar si el nombre en Fresha coincide exactamente con el nombre en la hoja Personas. Marcar como discrepancia y no como error. |

### Cruce C: Resultado operativo (Caja_diaria - Egresos)

| Aspecto | Detalle |
|---------|---------|
| **Qué cruza** | Ingresos totales (Caja_diaria) menos egresos totales (Egresos) por período |
| **Validación** | Resultado operativo diario y mensual |
| **Nivel de confianza del cruce** | Confirmado para Caja_diaria y Egresos por separado. La resta es un cálculo simple. |
| **Limitación** | Egresos.PersonaID frecuentemente vacío; no se puede atribuir resultado por persona todavía. |

### Cruce D: Descuentos en Fresha como análisis comercial

| Aspecto | Detalle |
|---------|---------|
| **Qué cruza** | Columna Descuentos en Fresha vs análisis de pricing |
| **Validación** | Tendencia de descuentos por período, por servicio, por canal |
| **Nivel de confianza del cruce** | Estimado — Los descuentos afectan ventas netas vs brutas, pero Sheets no tiene este desglose |
| **Limitación** | No hay forma de cruzar descuentos con Sheets porque Sheets no tiene ese dato |

---

## Cruces para después (requieren más relevamiento)

### Cruce E: Occupancy rate por barbero

| Qué necesita | Estado |
|--------------|--------|
| Servicios por barbero en Fresha / Horas disponibles en Fresha | **Futuro** — No hay acceso documentado a disponibilidad horaria en Fresha |
| Historial de occupancy por barbero | **Futuro** — Requiere datos que no se tienen todavía |

### Cruce F: Clientela nueva vs recurrente

| Qué necesita | Estado |
|--------------|--------|
| Campo "Cliente" en Fresha desglosado por nuevo/recurrente | **Futuro** — Fresha puede tener este dato, pero no está en el export estándar |
| Evolución histórica de nuevos vs recurrentes | **Futuro** — Requiere exportar múltiples períodos y comparar |

### Cruce G: ROI por promoción

| Qué necesita | Estado |
|--------------|--------|
| Ingresos en períodos con promoción (Fresha) vs sin promoción | **Futuro** — No hay forma de marcar períodos como "promocionales" en Sheets todavía |
| Egresos relacionados a la promoción (Egresos por categoría) | **Futuro** — Requiere identificar egresos promocionales, lo cual no está documentado |

### Cruce H: Proyección de caja a 30/60/90 días

| Qué necesita | Estado |
|--------------|--------|
| Historial de egresos por categoría (Egresos) | **Futuro** — Requiere datos consistentes de Egresos con categorización completa |
| Presupuesto (Stylos_Presupuesto) | **Parcial** — Hoja pendiente de relevar |
| Patrones estacionales | **Futuro** — Requiere al menos 12 meses de datos para inferir |

---

## Qué no se hace todavía

- **No se automatiza la exportación de Fresha.** Se hace manualmente cuando se necesita.
- **No se crean scripts de comparación.** La comparación se hace con ayuda de IA o manualmente en una hoja de cálculo.
- **No se propone PostgreSQL** para resolver las limitaciones de los cruces.
- **No se modifica Sheets** para facilitar los cruces. Se trabaja con lo que hay.
- **No se crea un dashboard** todavía. El análisis es bajo demanda, respondiendo a consultas específicas.

---

## Formato de documento de análisis cruzado

Cuando se realiza un análisis cruzado, el resultado se documenta así:

```markdown
## Análisis cruzado — [Nombre de la consulta]

### Fecha del análisis
[YYYY-MM-DD]

### Consulta original
[Texto de la consulta]

### Fuentes usadas
- [Fuente 1]: [qué se usó]
- [Fuente 2]: [qué se usó]

### Resumen por fuente
[Resumen breve de cada fuente]

### Hallazgos

#### Hallazgo 1
- **Qué se observó**: [hecho]
- **Fuentes**: [de dónde viene]
- **Nivel de confianza**: [confirmado / probable / estimado / no disponible]
- **Implicancia**: [qué significa para el negocio]

#### Hallazgo 2
...

### Discrepancias detectadas
- [Discrepancia 1]: [detalle]
- [Discrepancia 2]: [detalle]

### Recomendaciones
- [Recomendación 1]
- [Recomendación 2]

### Pendientes de verificar
- [Item 1]
- [Item 2]
```

---

## Referencias

- Método de consulta gerencial: `../03_procesos/metodo-consulta-gerencial.md`
- Fuentes de datos: `../02_modelo-datos/fuentes-analisis.md`
- Mapeo Fresha ↔ Sheets: `../02_modelo-datos/mapeo-fresha-sheets.md`
- Estructura de Sheets: `../02_modelo-datos/estructura-sheets.md`
- Diccionario de datos: `../02_modelo-datos/diccionario-datos.md`
- Plan de validaciones: `../02_modelo-datos/plan-validaciones-sheets.md`