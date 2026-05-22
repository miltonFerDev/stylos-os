# Plan de validaciones futuras — Google Sheets

## Objetivo del documento

Definir las validaciones que se aplicarán en el futuro a las hojas principales de `Stylos_Data` (Caja_diaria, Egresos y Comisiones), priorizarlas según impacto y dependencias, y dejar documentadas las hipótesis que deben confirmarse antes de implementar cualquier script o automatización.

Este documento no implementa nada. Solo planifica.

---

## Alcance

Hojas de `Stylos_Data` sujetas a validación:

- Caja_diaria
- Egresos
- Comisiones

Validaciones fuera de alcance por ahora:

- Hojas de diccionario (Personas, Categorías, Subcategorías, Medios de pago)
- Cuota parte, Presupuesto, Dashboard
- Cualquier automatización, script o migración a base de datos

---

## Caja_diaria

| ID | Campo o relación | Regla esperada | Tipo | Severidad | Acción sugerida | Estado |
|----|-----------------|----------------|------|-----------|-----------------|--------|
| V-CD-01 | Fecha | Obligatoria, formato uniforme (dd/mm/aaaa) | obligatoria | alta | Verificar formato real en Sheets | pendiente de confirmación |
| V-CD-02 | Periodo | Obligatorio; debe coincidir con año-mes de Fecha | consistencia | alta | Comparar Periodo vs提取 de Fecha | propuesta |
| V-CD-03 | Efectivo | Numérico, no negativo | obligatoria | alta | Verificar que sea numérico sin prefijo $ | propuesta |
| V-CD-04 | MPD | Numérico o vacío con significado definido | obligatoria | media | Confirmar si vacío = 0 o carga omitida | pendiente de confirmación |
| V-CD-05 | MPM | Numérico o vacío con significado definido | obligatoria | media | Confirmar si vacío = 0 o carga omitida; verificar si dejó de usarse ~jul 2025 | pendiente de confirmación |
| V-CD-06 | Tarjetas | Numérico o vacío con significado definido | obligatoria | media | Confirmar si vacío = 0 o carga omitida | pendiente de confirmación |
| V-CD-07 | Celdas vacías en medios de pago | Definir si vacío equivale a 0 o a carga omitida | consistencia | alta | Confirmar regla de negocio con usuario | pendiente de confirmación |
| V-CD-08 | Total Barbería | Debe coincidir con la suma de Efectivo + MPD + MPM + Tarjetas, si esa es la fórmula confirmada | cálculo | alta | Confirmar fórmula real en Sheets | pendiente de confirmación |
| V-CD-09 | Total Barbería = 0 | Alertar cuando Total = $0 para verificar si es día no trabajado vs error de carga | alerta | media | Revisar días con Total = 0 en CSV (filas 65, 122, 133) | propuesta |
| V-CD-10 | Fecha duplicada | No debe haber dos registros con la misma Fecha | consistencia | alta | Buscar duplicados por Fecha | propuesta |

---

## Egresos

| ID | Campo o relación | Regla esperada | Tipo | Severidad | Acción sugerida | Estado |
|----|-----------------|----------------|------|-----------|-----------------|--------|
| V-EG-01 | EgresoID | Obligatorio | obligatoria | alta | Verificar en Sheets | propuesta |
| V-EG-02 | EgresoID | Único (no duplicado) | consistencia | alta | Buscar IDs duplicados | propuesta |
| V-EG-03 | Fecha | Obligatoria, formato uniforme | obligatoria | alta | Verificar formato real en Sheets | propuesta |
| V-EG-04 | Periodo | Obligatorio; debe coincidir con año-mes de Fecha | consistencia | alta | Comparar Periodo vs extracción de Fecha | propuesta |
| V-EG-05 | Monto | Numérico, mayor a 0 | obligatoria | alta | Verificar tipo de dato y rango | propuesta |
| V-EG-06 | CategoriaID | Obligatorio; debe existir en hoja Categorías | diccionario | alta | Relevar hoja Categorías y contrastar | pendiente de confirmación |
| V-EG-07 | SubCategoriaID | Obligatorio; debe existir en hoja Subcategorías | diccionario | alta | Relevar hoja Subcategorías y contrastar | pendiente de confirmación |
| V-EG-08 | SubCategoriaID vs CategoriaID | SubCategoriaID debe ser hijo de CategoriaID | consistencia | media | Verificar estructura jerárquica en diccionarios | pendiente de confirmación |
| V-EG-09 | MedioPagoID | Obligatorio cuando aplique; debe existir en hoja Medios de pago | diccionario | media | Definir cuándo es obligatorio; relevar hoja Medios de pago | pendiente de confirmación |
| V-EG-10 | PersonaID | Obligatorio cuando corresponda; debe existir en hoja Personas | diccionario | media | Definir cuándo es obligatorio; relevar hoja Personas | pendiente de confirmación |
| V-EG-11 | Detalle en extraordinarios | Recomendado especialmente en egresos extraordinarios | alerta | baja | Sugerir en UI/carga sin imponer como error | propuesta |
| V-EG-12 | Detalle texto libre | Inconsistencias en Detalle son riesgo de carga manual, no errores necesariamente | alerta | baja | No imponer estandarización forzada; solo observar patrones | propuesta |

---

## Comisiones

| ID | Campo o relación | Regla esperada | Tipo | Severidad | Acción sugerida | Estado |
|----|-----------------|----------------|------|-----------|-----------------|--------|
| V-CO-01 | ComisionID | Obligatorio para registros nuevos (post ~nov 2025) | obligatoria | alta | Confirmar con usuario la política de ID para nuevos registros | pendiente de confirmación |
| V-CO-02 | Fecha | Obligatoria, formato uniforme | obligatoria | alta | Verificar formato real en Sheets | propuesta |
| V-CO-03 | Periodo | Obligatorio; debe coincidir con año-mes de Fecha | consistencia | alta | Comparar Periodo vs extracción de Fecha | propuesta |
| V-CO-04 | PersonaID | Obligatorio; debe existir en hoja Personas | diccionario | alta | Relevar hoja Personas y contrastar | pendiente de confirmación |
| V-CO-05 | Servicios | Numérico, entero, mayor o igual a 0 | obligatoria | alta | Verificar tipo de dato y rango | propuesta |
| V-CO-06 | Productos | Numérico, entero, o vacío con significado definido | obligatoria | media | Confirmar si vacío = 0 o no cargado | pendiente de confirmación |
| V-CO-07 | Comision | Numérica, no negativa | obligatoria | alta | Verificar tipo de dato y rango | propuesta |
| V-CO-08 | Total_Ventas | Posible campo calculado; pendiente confirmar fórmula (¿Servicios + Productos?) | cálculo | media | Verificar fórmula real en Sheets | pendiente de confirmación |
| V-CO-09 | Total_Abonado | Posible campo calculado; pendiente confirmar fórmula (¿Efectivo + MPD + MPM?) | cálculo | media | Verificar fórmula real en Sheets | pendiente de confirmación |
| V-CO-10 | Efectivo, MPD, MPM | Numéricos o vacío con significado definido | obligatoria | media | Confirmar si vacío = 0 o no cargado | pendiente de confirmación |
| V-CO-11 | Servicios = 0 y Comisión > 0 | Alerta (no error automático): verificar si corresponde a pago fijo, ajuste, retiro u otro concepto no estrictamente comisional | alerta | media | Revisar PersonaID=7 con Servicios=0 y Comisión fija ($43.000/$64.500) | pendiente de confirmación |

---

## Validaciones cruzadas propuestas — pendientes de confirmación

Las siguientes validaciones se identifican como potencialmente útiles pero requieren información que aún no se ha relevado. **No deben tratarse como reglas definidas.** Se incluyen aquí para no perder la pista de relaciones que podrían ser importantes una vez que se confirmen las dependencias entre hojas.

---

### V-CR-01: Día presente en Caja_diaria pero sin registros en Comisiones (o viceversa)

| Atributo | Detalle |
|----------|---------|
| **Relación que valida** | Cada día registrado en Caja_diaria debería corresponder al menos a un registro en Comisiones (y viceversa) |
| **Por qué podría ser útil** | Si un día hay ingresos en caja pero no hay comisiones cargadas, podría indicar que no se registró la actividad de los barbijos ese día |
| **Qué falta confirmar** | ¿Existe alguna regla de negocio que establezca esta correspondencia 1:1 o N:1? ¿Puede haber días con ingresos pero sin barberos? ¿O un barbero sin ingresos ese día? |
| **Estado** | Pendiente de confirmación |
| **Severidad tentativa** | Media |

---

### V-CR-02: Egresos.PersonaID referenciado en hoja Personas

| Atributo | Detalle |
|----------|---------|
| **Relación que valida** | Todo PersonaID usado en Egresos debería existir como registro en la hoja Personas |
| **Por qué podría ser útil** | Garantizar que no se asignen gastos a personas que no existen en el directorio |
| **Qué falta confirmar** | Contenido y estructura de la hoja Personas; si Egresos.PersonaID es optional, esta validación aplica solo cuando está presente |
| **Estado** | Pendiente de confirmación |
| **Severidad tentativa** | Alta |

---

### V-CR-03: Comisiones.PersonaID referenciado en hoja Personas

| Atributo | Detalle |
|----------|---------|
| **Relación que valida** | Todo PersonaID usado en Comisiones debería existir como registro en la hoja Personas |
| **Por qué podría ser útil** | Garantizar que las comisiones se atribuyen a barbijos reconocidos en el directorio |
| **Qué falta confirmar** | Contenido y estructura de la hoja Personas; si PersonaID en Comisiones es obligatorio (V-CO-04) |
| **Estado** | Pendiente de confirmación |
| **Severidad tentativa** | Alta |

---

### V-CR-04: CategoriaID y SubCategoriaID en Egresos referenciados en hojas diccionario

| Atributo | Detalle |
|----------|---------|
| **Relación que valida** | Los IDs de categoría y subcategoría usados en Egresos deberían existir en las hojas Categorías y Subcategorías |
| **Por qué podría ser útil** | Evitar que se carguen gastos con categorías que no existen, o con subcategorías que no pertenecen a la categoría angegeben |
| **Qué falta confirmar** | Estructura de las hojas Categorías y Subcategorías; si existe validación activa en Sheets |
| **Estado** | Pendiente de confirmación |
| **Severidad tentativa** | Alta |

---

### V-CR-05: Egreso en efectivo descuenta del Efectivo registrado en Caja_diaria

| Atributo | Detalle |
|----------|---------|
| **Relación que valida** | Si un egreso se paga en efectivo, debería reflejarse como una reducción del campo Efectivo en Caja_diaria del mismo día (o del período) |
| **Por qué podría ser útil** | Garantizar que el efectivo disponible en caja sea consistente con los gastos pagados en efectivo |
| **Qué falta confirmar** | No existe regla documentada para esta relación. No se sabe si los egresos en efectivo se registran como un flujo que afecta a Caja_diaria o si son independientes. Requiere entender el flujo de caja real antes de proponer cualquier validación |
| **Estado** | Pendiente de confirmación |
| **Severidad tentativa** | Baja |

---

## Prioridad de implementación

| Nivel | Descripción | Validaciones incluidas |
|-------|-------------|------------------------|
| **P1** | Verificable sin dependencias externas | V-CD-01, V-CD-02, V-CD-03, V-CD-09, V-CD-10, V-EG-01, V-EG-02, V-EG-03, V-EG-04, V-EG-05, V-CO-02, V-CO-03, V-CO-05, V-CO-07 |
| **P2** | Requiere confirmar hipótesis con usuario | V-CD-07, V-CD-08, V-EG-09, V-EG-10, V-CO-01, V-CO-06, V-CO-10, V-CO-11 |
| **P3** | Requiere relevar hojas diccionario | V-EG-06, V-EG-07, V-EG-08, V-CO-04, V-CR-02, V-CR-03, V-CR-04 |
| **P4** | Requiere fórmulas documentadas en Sheets | V-CO-08, V-CO-09 |

Las validaciones cruzadas (V-CR-01 a V-CR-05) no tienen nivel asignado porque dependen de información aún no relevada.

---

## Qué debe confirmarse antes de programar scripts

1. **Fórmula de Total Barbería** — ¿Es un `SUM` automático de Efectivo + MPD + MPM + Tarjetas o es un valor cargado manualmente?
2. **Fórmulas de Total_Ventas y Total_Abonado** — ¿De dónde se calculan? ¿De dónde sale el valor?
3. **Significado de celdas vacías en medios de pago** — ¿Empty significa $0 o significa que no se cargó el dato?
4. **Cuándo es obligatorio PersonaID en Egresos** — ¿Para todo egreso, solo para gastos personales, o queda a criterio del que carga?
5. **Cuándo es obligatorio MedioPagoID en Egresos** — ¿Para todo egreso o solo en ciertos casos?
6. **Contenido de las hojas diccionario** — Personas, Categorías, Subcategorías, Medios de pago (estructura y datos)
7. **Significado de PersonaID=7 con Servicios=0 y Comisión fija** — ¿Es un pago fijo, retiro, ajuste u otro concepto?
8. **Relación entre Egresos en efectivo y el campo Efectivo de Caja_diaria** — ¿Se descuenta automáticamente o son flujos independientes?

---

## Qué NO se implementa todavía

- Scripts de validación de ningún tipo
- Modificaciones a Google Sheets (validaciones de datos, listas desplegables, formato condicional, celdas protegidas)
- Automatización de procesos de carga o verificación
- Migración a PostgreSQL u otra base de datos
- Cambios en el proceso de carga actual de las planillas
- Reglas de negocio derivadas de las validaciones cruzadas (V-CR-01 a V-CR-05) mientras no estén confirmadas