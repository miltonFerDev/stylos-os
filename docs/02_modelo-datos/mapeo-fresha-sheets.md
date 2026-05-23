# Mapeo Fresha ↔ Google Sheets

## Objetivo

Mapear los campos del reporte `report_sales-log-detail` de Fresha (exportado manualmente en CSV) contra las hojas de Google Sheets. Este mapeo permite cruzar datos entre ambas fuentes para responder consultas gerenciales.

**Nota importante:** Toda relación inferida en este documento es preliminar y requiere validación contra las planillas reales antes de usarse como base para decisiones.

---

## Fuente: Fresha — report_sales-log-detail

### Campos conocidos del export CSV

| Campo Fresha | Tipo | Descripción |
|--------------|------|-------------|
| Fecha/Hora | Timestamp | Fecha y hora de la venta |
| Venta | Texto / ID | Identificador de la transacción en Fresha |
| Tipo | Texto | Tipo de registro: venta, reembolso, etc. |
| Artículo | Texto | Nombre del servicio o producto |
| Categoría | Texto | Categoría del artículo |
| Cliente | Texto | Nombre del cliente |
| Miembro del equipo | Texto | Barbero que realizó el servicio |
| Canal | Texto | Canal de reserva: online, mostrador, etc. |
| Ventas brutas | Monetario | Monto antes de descuentos |
| Descuentos | Monetario | Montos descontados |
| Ventas netas | Monetario | Ventas brutas menos descuentos |
| Total | Monetario | Monto final cobrado |

---

## Mapeo por campo

### Fecha/Hora ↔ Fecha en Sheets

| Fresha | Sheets | Relación | Estado |
|--------|--------|----------|--------|
| Fecha/Hora | Fecha (Caja_diaria) | Día igual | **Preliminar** — Requiere validar si Fresha usa zona horaria UTC y Sheets usa hora local |
| Fecha/Hora | Periodo (Caja_diaria, Egresos, Comisiones) | Coincidencia de año-mes | **Verificado** |
| Fecha/Hora | Fecha (Egresos) | Día igual | **Preliminar** — No todos los egresos tienen hora; solo fecha |
| Fecha/Hora | Fecha (Comisiones) | Día igual | **Preliminar** — No todas las comisiones tienen hora; solo fecha |

**Nota:** Fresha registra fecha y hora de la venta. Sheets (Caja_diaria, Egresos, Comisiones) usan solo fecha. La franja horaria podría ser útil para cross-validation pero no es directamente cruzable con Sheets por ahora.

---

### Miembro del equipo ↔ PersonaID

| Fresha | Sheets | Relación | Estado |
|--------|--------|----------|--------|
| Miembro del equipo | PersonaID (Comisiones) | Nombre del barbero → ID en hoja Personas | **Preliminar** — Requiere confirmar que el nombre en Fresha coincide exactamente con el nombre en la hoja Personas |
| Miembro del equipo | PersonaID (Egresos) | Algunos egresos tienen PersonaID (no todos) | **Parcial** — Egresos.PersonaID frecuentemente vacío |

**Nota:** No hay clave común documentada entre Fresha y Sheets. La relación se infiere por nombre de persona, lo cual es frágil (cambios de spelling, apodos, etc.).

---

### Ventas brutas / Ventas netas / Total ↔ Ingresos en Sheets

| Fresha | Sheets | Relación | Estado |
|--------|--------|----------|--------|
| Total | Total Barbería (Caja_diaria) | La suma de ventas de Fresha por día debería coincidir con Total Barbería en Sheets | **Hipótesis a confirmar** — No se ha verificado la coincidencia numérica |
| Ventas brutas | Campos individuales (EFECTIVO, MPD, MPM, Tarjetas) | Solo si Fresha desglosa por medio de pago | **No disponible** — Fresha no parece desglosar por medio de pago en el export estándar |
| Descuentos | Sin equivalente directo en Sheets | Análisis comercial | **Parcial** — Los descuentos pueden afectar la comparación de ventas netas vs totales |
| Total | Comision (Comisiones) | La suma de comisiones por día debería corresponderse | **Hipótesis a confirmar** |

**Nota:** Se desconoce si Fresha y Sheets registran exactamente la misma fecha. Por ejemplo, una venta registrada en Fresha a las 23:59 del lunes podría registrarse en Sheets el martes si hay demora en el cierre.

---

### Canal ↔ Sin equivalente directo en Sheets

| Fresha | Sheets | Relación | Estado |
|--------|--------|----------|--------|
| Canal | No existe | Fresha distingue entre reserva online, mostrador, etc. | **No disponible en Sheets** |
| Canal | Eventos (hipotético) | Podría documentarse como evento | **Futuro** |

---

### Cliente ↔ Sin equivalente en Sheets

| Fresha | Sheets | Relación | Estado |
|--------|--------|----------|--------|
| Cliente | No existe | Sheets no registra cliente individual en las hojas principales | **No disponible en Sheets** |
| Cliente | Fresha como CRM | Solo Fresha tiene el detalle de cliente por venta | **Fresha es la única fuente de cliente** |

---

### Categoría / Artículo ↔ Sin equivalente directo

| Fresha | Sheets | Relación | Estado |
|--------|--------|----------|--------|
| Categoría | No existe | En Sheets, los servicios no se categorizan por tipo | **No disponible en Sheets** |
| Artículo | No existe | En Sheets, el detalle de servicio no se individualiza | **No disponible en Sheets** |

---

## Cruces posibles entre Fresha y Sheets

### Cruce 1: Ventas diarias Fresha vs Total Barbería en Sheets

| Aspecto | Detalle |
|---------|---------|
| **Qué cruza** | Total de ventas por día en Fresha (suma de columna Total) vs Total Barbería en Caja_diaria |
| **Para qué sirve** | Validar consistencia entre ambas fuentes; detectar diferencias de carga o timing |
| **Estado** | **Hipótesis a confirmar** — Nunca se hizo la comparación real |
| **Dependencia** | Confirmar que la fecha de Fresha y la fecha de Sheets corresponden al mismo día de operación |

### Cruce 2: Miembro del equipo en Fresha vs Comisiones en Sheets

| Aspecto | Detalle |
|---------|---------|
| **Qué cruza** | Nombre del barbero en Fresha vs PersonaID en Comisiones |
| **Para qué sirve** | Verificar que los servicios en Fresha correspondan a las comisiones cargadas en Sheets |
| **Estado** | **Parcial** — Requiere verificar coincidencia de nombres |
| **Dependencia** | Que los nombres en Fresha coincidan con los nombres en la hoja Personas |

### Cruce 3: Servicios por barbero en Fresha vs Servicios en Comisiones

| Aspecto | Detalle |
|---------|---------|
| **Qué cruza** | Cantidad de servicios por barbero por día en Fresha vs Servicios en Comisiones |
| **Para qué sirve** | Cross-validation de actividad de barbijos |
| **Estado** | **Hipótesis a confirmar** |
| **Dependencia** | Que el nombre del barbero en Fresha matchee con PersonaID en Comisiones |

---

## Qué NO se puede cruzar todavía

| Cruce | Por qué no |
|-------|-----------|
| Fresha Canal ↔ Sheets | No hay campo equivalente en Sheets |
| Fresha Cliente ↔ Sheets | No hay registro de cliente en Sheets |
| Fresha Artículo ↔ Sheets | No hay detalle de servicio en Sheets |
| Fresha Descuentos ↔ Sheets | Sheets no tiene campo de descuentos |
| Fresha Hora ↔ Sheets | Sheets usa solo fecha, no hora |

---

## Limitaciones已知

1. **No hay clave común primaria.** La relación se hace por nombre de persona y fecha, ambos fragile.
2. **Fresha no desglosa por medio de pago.** No se puede compararEfectivo/MPD/MPM/Tarjeta entre Fresha y Sheets.
3. **Fresha tiene cliente individual; Sheets no.** La reconciliación a nivel cliente no es posible desde Sheets.
4. **Las fechas podrían no coincidir.** Una venta de último momento del lunes puede pasar a martes en Sheets.
5. **El formato del export CSV puede cambiar.** Fresha puede cambiar columnas o formato sin aviso.

---

## Qué hacer ante estas limitaciones

- **No asumir coincidencia perfecta.** Siempre validar antes de presentar una comparación como hecho.
- **Marcar las diferencias como hypotheses.** Si hay discrepancia, decir "posiblemente" y documentar elgap.
- **Usar Fresha como fuente primaria para actividad de servicios y cliente.** Usar Sheets para ingresos consolidados.
- **No forzar el cruce si los datos no alinean.** Si Fresha y Sheets dan números distintos para el mismo día, documentar la diferencia y no inventar una explicación.

---

## Referencias

- Fuentes de datos: `../02_modelo-datos/fuentes-analisis.md`
- Estructura de Sheets: `../02_modelo-datos/estructura-sheets.md`
- Diccionario de datos: `../02_modelo-datos/diccionario-datos.md`
- Cruza de datos: `../03_procesos/cruza-datos-inicial.md`