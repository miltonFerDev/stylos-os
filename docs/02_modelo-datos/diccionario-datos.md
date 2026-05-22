# Diccionario de datos

## Objetivo

Definir cada campo de datos utilizado en las hojas de Google Sheets de Stylo's Barber. Una sección por hoja, con tipo esperado, obligatoriedad, descripción, ejemplo y validaciones sugeridas.

Este documento se completa a medida que se relevan las planillas reales.

Estado posible: `documentado` / `pendiente` / `pendiente de verificación`

---

## Caja diaria

(Fuente: `Stylos_Data - Caja_diaria.csv` de muestra. Pendiente de verificar contra planilla real.)

| Campo | Tipo esperado | Obligatorio | Descripción | Ejemplo | Validaciones sugeridas | Estado |
|-------|---------------|-------------|-------------|---------|------------------------|--------|
| Fecha | Fecha (dd/mm/aaaa) | Sí | Fecha del día registrado | 2/1/2025 | Formato uniforme; no permitir fechas futuras | Documentado |
| Periodo | Texto (AAAA-MM) | Sí | Mes contable al que pertenece el día | 2025-01 | Debe coincidir con el año-mes de Fecha | Documentado |
| Efectivo | Numérico (monetario) | Sí | Ingresos en efectivo del día | 126000 | No negativo; consistencia con arqueo de caja | Documentado |
| MPD | Numérico (monetario) | No | Ingresos por Mercado Pago débito / cuotas | 17000 | No negativo; puede estar vacío si no hubo | Documentado |
| MPM | Numérico (monetario) | No | Ingresos por Mercado Pago mercado (QR, monedero, link de pago) | 72500 | No negativo; parece dejar de usarse ~julio 2025 | Documentado |
| Tarjetas | Numérico (monetario) | No | Ingresos por tarjetas de crédito / débito (no MP) | 40000 | No negativo; puede estar vacío | Documentado |
| Total Barbería | Numérico (monetario) | Sí | Suma total del día. **Posible campo calculado** (Efectivo + MPD + MPM + Tarjetas) | 255500 | Debe coincidir con la suma de los medios de pago | Documentado |

---

## Egresos

(Fuente: `Stylos_Data - Egresos.csv` de muestra. Pendiente de verificar contra planilla real.)

| Campo | Tipo esperado | Obligatorio | Descripción | Ejemplo | Validaciones sugeridas | Estado |
|-------|---------------|-------------|-------------|---------|------------------------|--------|
| EgresoID | Numérico / UUID | Sí | Identificador único del egreso | 1 (numérico) o a7f409f5 (UUID) | Formato según el período; no duplicado | Documentado |
| Fecha | Fecha (dd/mm/aaaa) | Sí | Fecha en que se realizó el egreso | 2/1/2025 | Formato uniforme; no permitir fechas futuras | Documentado |
| Periodo | Texto (AAAA-MM) | Sí | Mes contable del egreso | 2025-01 | Debe coincidir con el año-mes de Fecha | Documentado |
| Monto | Numérico (monetario) | Sí | Importe del egreso | 31731 | No negativo; formato numérico sin símbolo | Documentado |
| CategoriaID | Numérico (ID) | Sí | Identificador de la categoría del gasto. **Requiere diccionario/lista** (Categorías) | 2 | Debe existir en la hoja Categorías; no nulo | Documentado |
| SubCategoriaID | Numérico (ID) | Sí | Identificador de la subcategoría del gasto. **Requiere diccionario/lista** (Subcategorías) | 202 | Debe existir en la hoja Subcategorías; debe ser hijo de CategoriaID | Documentado |
| PersonaID | Numérico (ID) | No | Identificador de la persona relacionada al gasto. **Requiere diccionario/lista** (Personas) | 11 | Debe existir en la hoja Personas; puede estar vacío si el gasto no es personal | Documentado |
| MedioPagoID | Numérico (ID) | No | Identificador del medio de pago usado. **Requiere diccionario/lista** (Medios de pago) | 5 | Debe existir en la hoja Medios de pago; puede estar vacío en datos tempranos | Documentado |
| Detalle | Texto (libre) | No | Descripción opcional del egreso | Spotify | No contiene datos sensibles; usado de forma inconsistente | Documentado |

---

## Comisiones

(Fuente: `Stylos_Data - Comisiones.csv` de muestra. Pendiente de verificar contra planilla real.)

| Campo | Tipo esperado | Obligatorio | Descripción | Ejemplo | Validaciones sugeridas | Estado |
|-------|---------------|-------------|-------------|---------|------------------------|--------|
| ComisionID | UUID / vacío | No | Identificador único de la comisión. Vacío en datos tempranos | (vacío) o 94389a6e | Consistencia de formato según período | Documentado |
| Fecha | Fecha (dd/mm/aaaa) | Sí | Día laboral registrado | 2/1/2025 | Formato uniforme; no permitir fechas futuras | Documentado |
| Periodo | Texto (AAAA-MM) | Sí | Mes contable | 2025-01 | Debe coincidir con el año-mes de Fecha | Documentado |
| PersonaID | Numérico (ID) | Sí | Identificador del barbero. **Requiere diccionario/lista** (Personas) | 7 | Debe existir en la hoja Personas | Documentado |
| Servicios | Numérico (entero) | Sí | Cantidad de servicios realizados | 4 | No negativo; entero | Documentado |
| Productos | Numérico (entero) | No | Cantidad de productos vendidos | (vacío) o 1 | No negativo; entero; usado de forma inconsistente | Documentado |
| Comision | Numérico (monetario) | Sí | Monto de la comisión del barbero | 14400 | No negativo | Documentado |
| Total Ventas | Numérico (entero) | Sí | Suma de Servicios + Productos. **Posible campo calculado** | 4 | Debe coincidir con la suma de Servicios + Productos | Documentado |
| Efectivo | Numérico (monetario) | No | Porción cobrada en efectivo | 20000 | No negativo; puede estar vacío (casi siempre vacío hasta ~ago 2025) | Documentado |
| MPD | Numérico (monetario) | No | Porción cobrada por Mercado Pago débito | 14400 | No negativo; puede estar vacío | Documentado |
| MPM | Numérico (monetario) | No | Porción cobrada por Mercado Pago mercado | 26400 | No negativo; puede estar vacío | Documentado |
| Total Abonado | Numérico (monetario) | No | Suma cobrada. **Posible campo calculado** (Efectivo + MPD + MPM) | 46400 | Debe coincidir con la suma de los medios cobrados | Documentado |

---

## Cuota parte

| Campo | Tipo esperado | Obligatorio | Descripción | Ejemplo | Validaciones sugeridas | Estado |
|-------|---------------|-------------|-------------|---------|------------------------|--------|
| TODO | TODO | TODO | TODO | TODO | TODO | Pendiente |
| TODO | TODO | TODO | TODO | TODO | TODO | Pendiente |

---

## Presupuesto

| Campo | Tipo esperado | Obligatorio | Descripción | Ejemplo | Validaciones sugeridas | Estado |
|-------|---------------|-------------|-------------|---------|------------------------|--------|
| TODO | TODO | TODO | TODO | TODO | TODO | Pendiente |
| TODO | TODO | TODO | TODO | TODO | TODO | Pendiente |

---

## Dashboard

| Campo | Tipo esperado | Obligatorio | Descripción | Ejemplo | Validaciones sugeridas | Estado |
|-------|---------------|-------------|-------------|---------|------------------------|--------|
| TODO | TODO | TODO | TODO | TODO | TODO | Pendiente |
| TODO | TODO | TODO | TODO | TODO | TODO | Pendiente |

---

## Personas

| Campo | Tipo esperado | Obligatorio | Descripción | Ejemplo | Validaciones sugeridas | Estado |
|-------|---------------|-------------|-------------|---------|------------------------|--------|
| TODO | TODO | TODO | TODO | TODO | TODO | Pendiente |
| TODO | TODO | TODO | TODO | TODO | TODO | Pendiente |

---

## Categorías

| Campo | Tipo esperado | Obligatorio | Descripción | Ejemplo | Validaciones sugeridas | Estado |
|-------|---------------|-------------|-------------|---------|------------------------|--------|
| TODO | TODO | TODO | TODO | TODO | TODO | Pendiente |
| TODO | TODO | TODO | TODO | TODO | TODO | Pendiente |

---

## Subcategorías

| Campo | Tipo esperado | Obligatorio | Descripción | Ejemplo | Validaciones sugeridas | Estado |
|-------|---------------|-------------|-------------|---------|------------------------|--------|
| TODO | TODO | TODO | TODO | TODO | TODO | Pendiente |
| TODO | TODO | TODO | TODO | TODO | TODO | Pendiente |

---

## Medios de pago

| Campo | Tipo esperado | Obligatorio | Descripción | Ejemplo | Validaciones sugeridas | Estado |
|-------|---------------|-------------|-------------|---------|------------------------|--------|
| TODO | TODO | TODO | TODO | TODO | TODO | Pendiente |
| TODO | TODO | TODO | TODO | TODO | TODO | Pendiente |

---

## Eventos

| Campo | Tipo esperado | Obligatorio | Descripción | Ejemplo | Validaciones sugeridas | Estado |
|-------|---------------|-------------|-------------|---------|------------------------|--------|
| TODO | TODO | TODO | TODO | TODO | TODO | Pendiente |
| TODO | TODO | TODO | TODO | TODO | TODO | Pendiente |

---

## Decisiones

| Campo | Tipo esperado | Obligatorio | Descripción | Ejemplo | Validaciones sugeridas | Estado |
|-------|---------------|-------------|-------------|---------|------------------------|--------|
| TODO | TODO | TODO | TODO | TODO | TODO | Pendiente |
| TODO | TODO | TODO | TODO | TODO | TODO | Pendiente |

---

## Consultas IA

| Campo | Tipo esperado | Obligatorio | Descripción | Ejemplo | Validaciones sugeridas | Estado |
|-------|---------------|-------------|-------------|---------|------------------------|--------|
| TODO | TODO | TODO | TODO | TODO | TODO | Pendiente |
| TODO | TODO | TODO | TODO | TODO | TODO | Pendiente |

---

## Aprendizajes

| Campo | Tipo esperado | Obligatorio | Descripción | Ejemplo | Validaciones sugeridas | Estado |
|-------|---------------|-------------|-------------|---------|------------------------|--------|
| TODO | TODO | TODO | TODO | TODO | TODO | Pendiente |
| TODO | TODO | TODO | TODO | TODO | TODO | Pendiente |
