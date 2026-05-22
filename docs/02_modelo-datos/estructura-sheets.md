# Estructura de Google Sheets

## Objetivo del documento

Mapear los archivos y hojas de Google Sheets que usa Stylo's Barber, entender su función, cómo se relacionan y qué datos contienen. Este documento es la base para futuras auditorías, mejoras y eventuales migraciones.

No modifica ni propone cambios en las planillas. Solo documenta lo que existe y lo que falta relevar.

---

## Archivos conocidos

| Archivo | Función esperada | URL | Estado |
|---------|------------------|-----|--------|
| `Stylos_Data` | Registro de datos crudos del negocio: caja diaria, egresos, comisiones, personas, categorías, medios de pago | PENDIENTE | Se confirmó existencia por CSV de muestra |
| `Stylos_Analisis` | Procesamiento, fórmulas y dashboard sobre los datos de `Stylos_Data` | PENDIENTE | Pendiente de relevar |
| `Stylos_Presupuesto` | Presupuesto mensual/anual, proyecciones y control de desvíos | PENDIENTE | Pendiente de relevar |

PENDIENTE: Confirmar nombres exactos y URLs de cada archivo.

---

## Hojas conocidas o esperadas

| Hoja | Función esperada | Archivo contenedor | Tipo | Frecuencia de carga |
|------|------------------|--------------------|------|---------------------|
| Caja diaria | Registro de ingresos diarios por medios de pago | `Stylos_Data` | Dato crudo | Diaria |
| Egresos | Detalle de gastos del negocio | `Stylos_Data` | Dato crudo | Diaria / Semanal |
| Comisiones | Cálculo de comisiones por barbero por día | `Stylos_Data` | Dato crudo | Diaria |
| Cuota parte | Distribución de ingresos por cuota parte | PENDIENTE | Análisis | Mensual |
| Presupuesto | Presupuesto vigente y ejecución | `Stylos_Presupuesto` | Análisis | Mensual |
| Dashboard | Indicadores resumen del negocio | `Stylos_Analisis` | Análisis | Bajo demanda |
| Personas | Barberos y participantes del negocio | PENDIENTE | Dato crudo | Eventual |
| Categorías | Clasificación de ingresos/egresos | PENDIENTE | Dato crudo | Eventual |
| Subcategorías | Detalle de clasificación por categoría | PENDIENTE | Dato crudo | Eventual |
| Medios de pago | Medios de pago aceptados y su configuración | PENDIENTE | Dato crudo | Eventual |
| Eventos | Registro de eventos relevantes del negocio | PENDIENTE | Dato crudo | Según ocurran |
| Decisiones | Registro de decisiones tomadas | PENDIENTE | Memoria | Según ocurran |
| Consultas IA | Preguntas y respuestas con IA | PENDIENTE | Memoria | Según ocurran |
| Aprendizajes | Lecciones aprendidas validadas | PENDIENTE | Memoria | Según ocurran |

Nota: Caja diaria, Egresos y Comisiones se confirmaron como hojas de `Stylos_Data` mediante CSV de muestra.

PENDIENTE: Confirmar archivo contenedor de Cuota parte, Personas, Categorías, Subcategorías, Medios de pago, Eventos, Decisiones, Consultas IA y Aprendizajes.

---

## Datos crudos vs. análisis

Se identifican dos categorías de datos en las planillas:

### Datos crudos

Ingresan manualmente al sistema (desde caja diaria, Fresha, WhatsApp, etc.):

- Caja diaria
- Egresos
- Comisiones
- Personas
- Categorías
- Subcategorías
- Medios de pago
- Eventos
- Decisiones
- Consultas IA
- Aprendizajes

### Datos de análisis

Se generan a partir de fórmulas sobre los datos crudos:

- Cuota parte
- Presupuesto (ejecución vs. presupuestado)
- Dashboard

PENDIENTE: Verificar si existen otras hojas de cálculo o tablas de referencia no listadas.

---

## Relaciones entre archivos y hojas

PENDIENTE: Este es el punto más crítico del relevamiento. Se necesita identificar:

- Qué hojas de `Stylos_Data` alimentan a `Stylos_Analisis`
- Qué hojas de `Stylos_Analisis` alimentan al Dashboard
- Si `Stylos_Presupuesto` toma datos de `Stylos_Data` o se alimenta por separado
- Si existen referencias cruzadas entre hojas (ej: `Egresos` → `Caja diaria`)
- Dependencias de fórmulas entre celdas de distintas hojas

---

## Observaciones preliminares

Inferidas del análisis de CSV de muestra (`data/raw/samples/`). Verificar contra planillas reales.

### Sobre Caja diaria

- `Total Barbería` parece un campo calculado (suma de Efectivo + MPD + MPM + Tarjetas)
- `MPD` (Mercado Pago débito/cuotas), `MPM` (Mercado Pago mercado/monedero) y `Tarjetas` (tarjetas de crédito/débito) son los medios de pago registrados
- MPM deja de tener valores ~julio 2025 (cambia a vacío/0)
- Algunos días registran Total = $0 (día sin actividad o día no trabajado)
- Hay celdas vacías en MPD, MPM y Tarjetas que podrían ser 0 implícitos o carga omitida
- ~enero 2026 cambia el formato: los valores pierden el prefijo `$`

### Sobre Egresos

- Requiere diccionarios auxiliares para CategoriaID, SubCategoriaID, PersonaID y MedioPagoID
- CategoriaID agrupa SubCategoriaID (estructura jerárquica: categorías → subcategorías)
- PersonaID frecuentemente vacío: sugiere que no todos los egresos se asignan a una persona
- MedioPagoID frecuentemente vacío en datos tempranos: puede indicar medio de pago por defecto
- `Detalle` es texto libre, usado de forma inconsistente (comentarios, aclaraciones de pagos parciales)
- ~enero 2026: EgresoID cambia de numérico secuencial a UUID, valores monetarios pierden prefijo `$`

### Sobre Comisiones

- `Comision` es el monto calculado por barbero; parece basado en la cantidad de servicios
- `Total_Ventas` parece calculado como Servicios + Productos
- `Total_Abonado` parece calculado como Efectivo + MPD + MPM
- PersonaID=7 con Servicios=0 aparece con alta frecuencia: posible pago fijo, no comisión variable
- Los campos de desglose de pago (Efectivo, MPD, MPM, Total_Abonado) se agregan ~agosto 2025
- ComisionID vacío en datos tempranos (hasta ~nov 2025), luego UUID

### Generales

- El cambio de formato y de sistema de IDs ~diciembre 2025 / enero 2026 sugiere un cambio en la herramienta de carga (posible migración a formulario Google Forms o similar)
- Los diccionarios auxiliares (Personas, Categorías, Subcategorías, Medios de pago) son críticos para interpretar los IDs
- El archivo de muestra confirma que los nombres de hoja contienen espacios (ej: "Stylos_Data - Caja_diaria")

---

## Pendientes de relevamiento

- [x] Confirmar nombres exactos de los 3 archivos de Sheets (parcial: se confirmó Sty los_Data)
- [ ] Obtener URLs de cada archivo
- [x] Confirmar qué hojas existen realmente en cada archivo (parcial: Caja_diaria, Egresos, Comisiones confirmadas en Sty los_Data)
- [x] Identificar columnas reales de Caja_diaria, Egresos y Comisiones (ver `diccionario-datos.md`)
- [ ] Identificar columnas reales de Cuota parte, Presupuesto, Dashboard, Personas, Categorías, Subcategorías, Medios de pago, Eventos, Decisiones, Consultas IA, Aprendizajes
- [ ] Mapear relaciones entre hojas
- [ ] Identificar fórmulas críticas
- [ ] Identificar validaciones actuales en Sheets
- [ ] Verificar si existen archivos adicionales no listados
- [ ] Confirmar frecuencia real de actualización de cada hoja
- [ ] Verificar contra planillas reales las observaciones preliminares
