# Auditoría preliminar de calidad de datos

## Limitaciones del análisis

- El análisis se basa exclusivamente en los CSV de referencia ubicados en `data/raw/samples/`.
- Los CSV pueden no reflejar las fórmulas reales de Google Sheets ni los formatos de celda aplicados en el archivo original.
- No se evaluó exactitud financiera de ningún registro.
- No se modificaron datos en ningún paso del análisis.
- Todo hallazgo marcado como "Hipótesis a confirmar" u "Observación preliminar" debe verificarse contra las planillas reales antes de convertirse en reglas de validación o automatización.

---

## Objetivo

Identificar riesgos de calidad de datos en las hojas principales de `Stylos_Data` (Caja_diaria, Egresos, Comisiones) para reducir errores antes de cualquier carga, migración o análisis automatizado.

## Alcance

Hojas del archivo `Stylos_Data`:
- Caja_diaria
- Egresos
- Comisiones

## Metodología

1. Inspección visual de los CSV de muestra en `data/raw/samples/`.
2. Contraste contra el diccionario de datos existente (`diccionario-datos.md`).
3. Detección de anomalías: celdas vacías, totales inconsistentes, cambios de formato, ids faltantes.
4. Clasificación de riesgos: formato, completitud, consistencia, dependencias.
5. Cada anomalía se clasifica como:
   - **Hipótesis a confirmar**: inferencia que requiere verificación en la hoja real.
   - **Observación preliminar**: patrón observado que no constituye necesariamente un error.

---

## Caja_diaria

### 1. Función de la hoja

Registra el movimiento diario de la barbería desglosado por medio de cobro (Efectivo, MPD, MPM, Tarjetas) y el total calculado por día.

### 2. Campos críticos

| Campo | Riesgo observado |
|-------|-----------------|
| Fecha | Formato variado (D/M/AAAA vs AAAA-MM-DD) — ver sección 4 |
| Total Barbería | Posible campo calculado — fórmula no documentada |

### 3. Campos posiblemente calculados

- **Total Barbería**: Observación preliminar — el campo parece ser la suma de Efectivo + MPD + MPM + Tarjetas, pero no está documentada la fórmula. Hipótesis a confirmar: se trata de un `SUM` de las columnas de medios o de un total cargado manualmente.

### 4. Campos que dependen de diccionarios/listas

- Ninguno identificado en esta hoja. Todos los campos son numéricos o de fecha.

### 5. Validaciones recomendadas

| # | Validación | Estado actual | Hipótesis |
|---|-----------|---------------|-----------|
| 1 | La suma de Efectivo + MPD + MPM + Tarjetas debe coincidir con Total Barbería | No está documentada todavía la fórmula o regla de validación que confirma que la suma de medios coincida con Total Barbería | Hipótesis a confirmar |
| 2 | Días con Total = $0 | Se observaron 3 días con Total = $0 (2/4/2025, 24/6/2025, 9/7/2025) | Hipótesis a confirmar: pueden ser días no trabajados o carga omitida |
| 3 | Celdas vacías vs $0 en medios de pago | Se detectaron 29 filas con celdas vacías en MPD, MPM o Tarjetas | Hipótesis a confirmar: una celda vacía puede significar $0 o carga omitida |
| 4 | Consistencia de formato monetario | Cambio de prefijo `$` a sin prefijo ~enero 2026 | Observación preliminar — no constituye error por sí solo |

### 6. Riesgos de carga manual

- **Riesgo medio**: Total Barbería podría ingresarse manualmente sin que se valide contra la suma de columnas. En caso de error, no habría forma de detectarlo automáticamente.
- **Riesgo bajo**: Celdas vacías en vez de `$0` en medios de pago pueden generar cálculos inconsistentes en análisis posteriores.

### 7. Dudas pendientes

- ¿Los días con Total = $0 corresponden a días no trabajados o son errores de carga?
- ¿La fórmula de Total Barbería es un `SUM` automático de Google Sheets o es un valor digitado?
- ¿Cuál es la regla de negocio para registrar un día como "$0" vs no registrarlo?

### 8. Prioridad de mejora

**Alta** — La falta de validación entre medios y total puede generar errores silenciosos en los reportes.

---

## Egresos

### 1. Función de la hoja

Registra los gastos del local desglosados por categoría, subcategoría, medio de pago, fecha y persona responsable.

### 2. Campos críticos

| Campo | Riesgo observado |
|-------|-----------------|
| PersonaID | Alto porcentaje de campos vacíos en los registros analizados — ver sección 5 |
| MedioPagoID | Varios registros con campo vacío en datos temprana |
| EgresoID | Cambio de formato de numérico a UUID sin migración de datos anteriores |

### 3. Campos posiblemente calculados

- Ninguno identificado con certeza. Verificar contra formulas reales en Sheets.

### 4. Campos que dependen de diccionarios/listas

- **CategoriaID**: Observación preliminar — los valores encontrados (1 a 8) parecen corresponder a una lista externa. Sin validación visible en CSV contra un diccionario.
- **SubCategoriaID**: Misma observación. Los valores (101, 102, 201, etc.) dependen de CategoriaID.
- **MedioPagoID**: Misma observación.
- **PersonaID**: Misma observación.

### 5. Validaciones recomendadas

| # | Validación | Estado actual | Hipótesis |
|---|-----------|---------------|-----------|
| 1 | Todo gasto debe tener PersonaID | Se observó un alto porcentaje de campos vacíos en los registros analizados | Hipótesis a confirmar: la ausencia de PersonaID podría ser válida (gastos generales) o un error de carga |
| 2 | Todo gasto debe tener MedioPagoID | Se detectaron registros con MedioPagoID vacío en datos temprana | Hipótesis a confirmar |
| 3 | EgresoID único | Se observó cambio de formato numérico a UUID sin limpieza de IDs antiguos | Observación preliminar |
| 4 | CategoriaID existe en diccionario | Valores observados entre 1 y 8, rango plausible pero sin validación | Hipótesis a confirmar |
| 5 | SubCategoriaID existe en diccionario | Valores observados (101, 102, 201, 301, etc.) sin validación | Hipótesis a confirmar |
| 6 | Detalle es texto libre | Se observaron valores breves, a veces vacíos, a veces descriptivos | Observación preliminar: la inconsistencia en Detalle es un riesgo de carga manual, no un error necesariamente |

### 6. Riesgos de carga manual

- **Riesgo alto**: Si PersonaID es required pero se deja vacío frecuentemente, los reportes de gastos por persona estarán incompletos.
- **Riesgo medio**: Detalle自由的自由文本可能导致描述不一致（例如 "Alq" vs "Alquiler" vs 空），使后续分析变得困难。
- **Riesgo medio**: Cambio de EgresoID sin migración puede afectar fórmulas que referencian IDs antiguos.

### 7. Dudas pendientes

- ¿PersonaID vacío es un comportamiento esperado (gastos generales) o un error de carga?
- ¿Qué representa el campo Detalle? ¿Debería ser obligatorio o自由文本？
- ¿El cambio de EgresoID a UUID fue accidental o intencional?
- ¿Existe una regla que determine qué PersonaID corresponde a qué tipo de gasto?

### 8. Prioridad de mejora

**Alta** — La falta de PersonaID en múltiples registros dificulta la atribución de gastos. La ausencia de validación contra diccionarios permite valores inválidos sin alerta.

---

## Comisiones

### 1. Función de la hoja

Registra comisiones de los barbijos por servicio realizado, con desglose de ventas, abonos y forma de pago.

### 2. Campos críticos

| Campo | Riesgo observado |
|-------|-----------------|
| PersonaID | Alto porcentaje de campos vacíos en registros temprana — ver sección 5 |
| ComisionID | Alto porcentaje de campos vacíos en registros temprana — ver sección 5 |
| Total_Ventas | Posible campo calculado — fórmula no documentada |
| Total_Abonado | Posible campo calculado — fórmula no documentada |

### 3. Campos posiblemente calculados

- **Total_Ventas**: Observación preliminar — parece ser un valor calculado o cargado que representa el total de ventas del día. Fórmula no documentada.
- **Total_Abonado**: Observación preliminar — misma situación.
- **Servicios**: Observación preliminar — podría ser un conteo o un total de servicios facturados. Fórmula no documentada.

### 4. Campos que dependen de diccionarios/listas

- **PersonaID**: Depende de la hoja Personas. Verificar si la referencia es obligatoria.
- **ComisionID**: No se identificó un diccionario asociado.

### 5. Validaciones recomendadas

| # | Validación | Estado actual | Hipótesis |
|---|-----------|---------------|-----------|
| 1 | Todo registro debe tener ComisionID | Se observó que en los registros tempranaanalizados, ComisionID estaba vacío | Hipótesis a confirmar: el alto porcentaje de vacíos es una estimación basada en el CSV analizado |
| 2 | Todo registro debe tener PersonaID | Se observó un alto porcentaje de campos vacíos en los registros tempranaanalizados | Hipótesis a confirmar: misma situación |
| 3 | Servicios = 0 con PersonaID=7 recurrente | Se detectaron múltiples registros con PersonaID=7, Servicios=0 y Comisión fija ($43.000 o $64.500) | Hipótesis a confirmar: PersonaID=7 aparece asociado a registros con Servicios=0 y Comisión fija. Podría representar un pago fijo, ajuste, retiro u otro concepto no estrictamente comisional |
| 4 | Suma de abonos (Efectivo + MPD + MPM) debe coincidir con Total_Abonado | No se identificó validación visible | Hipótesis a confirmar |
| 5 | Total_Ventas y Total_Abonado son consistentes entre sí | No se identificó validación visible | Hipótesis a confirmar |

### 6. Riesgos de carga manual

- **Riesgo alto**: PersonaID vacío impede trackear a quién corresponde la comisión.
- **Riesgo medio**: Si ComisionID es el identificador único y está vacío en muchos registros, la deduplicación es imposible.
- **Riesgo medio**: La mezcla de texto libre (Detalle) y números (Monto) en el mismo campo puede generar errores de parsing.

### 7. Dudas pendientes

- ¿PersonaID vacío es un error de carga o un registro sin barbijos ese día?
- ¿Qué representa PersonaID=7 con Servicios=0? ¿Es un pago fijo recurrente?
- ¿Cuál es la fórmula real de Total_Ventas y Total_Abonado?
- ¿Qué significa Servicios = 0 en el contexto de Comisiones?

### 8. Prioridad de mejora

**Media** — La falta de ComisionID y PersonaID en muchos registros es una сигнал de alerta. La relación entre Servicios=0 y PersonaID=7 requiere verificación urgente para entender si esas comisiones son válidas.

---

## Resumen de prioridades

| Hoja | Prioridad | Principal riesgo |
|------|----------|-----------------|
| Caja_diaria | Alta | Sin validación de que suma de medios = Total Barbería |
| Egresos | Alta | Alto % de PersonaID vacío; sin validación contra diccionarios |
| Comisiones | Media | PersonaID y ComisionID vacíos;不明白 PersonaID=7 |

---

## Próximos pasos

1. **Verificar contra Sheets reales** cada anomalía marcada como "Hipótesis a confirmar".
2. **Documentar fórmulas reales** de Total Barbería, Total_Ventas y Total_Abonado.
3. **Confirmar con el usuario** si PersonaID vacío es válido o un error de carga.
4. **Decidir** si se implementan validaciones en Sheets (listas desplegables, formato condicional) o se mantiene el proceso actual.
5. **Evaluar** la necesidad de un diccionario de PersonaID para estandarizar la atribución de gastos y comisiones.