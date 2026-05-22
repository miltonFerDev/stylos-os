# Pendientes de relevamiento — Google Sheets

## Objetivo

Listar toda la información que falta relevar sobre las planillas de Google Sheets. Cada ítem se marca como completado cuando se verifica contra la planilla real.

---

## Archivos

- [x] Confirmar nombre exacto del archivo de datos crudos (referido como `Stylos_Data`) — confirmado por CSV de muestra
- [ ] Confirmar nombre exacto del archivo de análisis (referido como `Stylos_Analisis`)
- [ ] Confirmar nombre exacto del archivo de presupuesto (referido como `Stylos_Presupuesto`)
- [ ] Verificar si existen archivos adicionales no listados
- [ ] Obtener URLs de cada archivo (sin commitear si contienen claves o tokens)
- [ ] Registrar frecuencia de modificación de cada archivo

## Hojas

- [x] Confirmar hojas Caja_diaria, Egresos y Comisiones dentro de `Stylos_Data` — confirmado por CSV de muestra
- [ ] Confirmar hojas reales dentro de `Stylos_Analisis`
- [ ] Confirmar hojas reales dentro de `Stylos_Presupuesto`
- [ ] Identificar hojas ocultas o de cálculo auxiliar
- [ ] Identificar si existen hojas duplicadas o versiones anteriores

## Columnas

- [x] Relevar columnas reales de Caja diaria (ver `diccionario-datos.md`)
- [x] Relevar columnas reales de Egresos (ver `diccionario-datos.md`)
- [x] Relevar columnas reales de Comisiones (ver `diccionario-datos.md`)
- [ ] Relevar columnas reales de Cuota parte
- [ ] Relevar columnas reales de Presupuesto
- [ ] Relevar columnas reales de Dashboard
- [ ] Relevar columnas reales de Personas
- [ ] Relevar columnas reales de Categorías
- [ ] Relevar columnas reales de Subcategorías
- [ ] Relevar columnas reales de Medios de pago
- [ ] Relevar columnas reales de Eventos
- [ ] Relevar columnas reales de Decisiones
- [ ] Relevar columnas reales de Consultas IA
- [ ] Relevar columnas reales de Aprendizajes

## Fórmulas

- [ ] Identificar fórmulas críticas en el archivo de análisis
- [ ] Identificar fórmulas en Cuota parte
- [ ] Identificar fórmulas en Dashboard
- [ ] Identificar referencias entre hojas (ej: `=Stylos_Data!...`)
- [ ] Identificar fórmulas en Presupuesto (si existen)
- [ ] Evaluar si hay fórmulas con errores o rotas

## Dependencias

- [ ] Mapear qué hojas de `Stylos_Data` usa `Stylos_Analisis`
- [ ] Mapear qué hojas de `Stylos_Analisis` usa el Dashboard
- [ ] Mapear dependencias de `Stylos_Presupuesto` con otros archivos
- [ ] Identificar dependencias entre hojas dentro del mismo archivo
- [ ] Identificar si hay dependencias circulares

## Validaciones actuales

- [ ] Identificar validaciones de datos existentes en Sheets (menús desplegables, rangos permitidos, etc.)
- [ ] Identificar celdas con formato condicional y su lógica
- [ ] Identificar celdas bloqueadas o protegidas
- [ ] Identificar rangos con permisos restringidos

## Problemas conocidos

- [ ] Preguntar: ¿hay errores conocidos en alguna hoja?
- [ ] Preguntar: ¿hay datos inconsistentes o duplicados?
- [ ] Preguntar: ¿hay hojas o columnas que ya no se usan?
- [ ] Preguntar: ¿hay procesos manuales propensos a error?
- [ ] Preguntar: ¿hay datos que deban estar pero no están?

## Mejoras posibles

(solo anotar, no implementar)

- [ ] Anotar si alguna hoja necesita nuevas columnas
- [ ] Anotar si algún cálculo manual podría automatizarse
- [ ] Anotar si faltan validaciones en campos críticos
- [ ] Anotar si la estructura dificulta el análisis posterior
- [ ] Anotar si hay información duplicada entre hojas

---

## Nuevos pendientes detectados tras el análisis de CSV

Estos ítems se agregaron a partir del análisis de los CSV de muestra en `data/raw/samples/`.

### Formato y estructura

- [ ] Verificar contra planilla real el cambio de formato ~enero 2026 (IDs numéricos a UUID, valores sin `$`) — Observación preliminar
- [ ] Confirmar si MPM (Mercado Pago mercado) dejó de usarse realmente ~julio 2025 — Hipótesis a confirmar

### Caja_diaria

- [ ] Confirmar si Total Barbería en Caja_diaria es un campo calculado (SUM de columnas) o se carga manualmente — Hipótesis a confirmar
- [ ] Verificar si los días con Total = $0 (filas 65, 122, 133 del CSV) son días no trabajados o errores de carga — Hipótesis a confirmar
- [ ] Confirmar si celdas vacías en MPD, MPM o Tarjetas significan $0 o carga omitida — Hipótesis a confirmar
- [ ] Documentar la fórmula (si existe) que valida que la suma de medios coincida con Total Barbería

### Egresos

- [ ] Confirmar si PersonaID vacío es comportamiento válido (gastos generales sin responsable) o error de carga — Hipótesis a confirmar (estimación basada en CSV)
- [ ] Verificar qué representa el campo Detalle y si debería estandarizarse — Observación preliminar
- [ ] Confirmar si CategoriaID, SubCategoriaID y MedioPagoID tienen validación contra diccionarios — Hipótesis a confirmar
- [ ] Investigar si el cambio de EgresoID de numérico a UUID fue intencional o accidental
- [ ] Verificar qué significa MedioPagoID vacío en registros temprana (posible dato faltante vs válido) — Hipótesis a confirmar

### Comisiones

- [ ] Confirmar si Total_Ventas y Total_Abonado son campos calculados y cuál es su fórmula — Hipótesis a confirmar
- [ ] Investigar PersonaID=7 con Servicios=0 y Comisión fija ($43.000/$64.500): podría representar un pago fijo, ajuste, retiro u otro concepto no estrictamente comisional — Hipótesis a confirmar
- [ ] Confirmar si PersonaID y ComisionID vacíos en registros temprana son errores de carga — Hipótesis a confirmar (estimación basada en CSV)
- [ ] Verificar qué significa Servicios = 0 en el contexto de Comisiones

### Diccionarios

- [ ] Verificar la estructura de las hojas diccionario: Personas, Categorías, Subcategorías, Medios de pago
- [ ] Identificar qué representan las PersonaID más recurrentes en Egresos y Comisiones
- [ ] Confirmar si existe un diccionario para ComisionID

---

## Historial de relevamiento

| Fecha | Ítems completados | Próximo paso |
|-------|-------------------|-------------|
| 2026-05-21 | Columnas de Caja diaria, Egresos y Comisiones relevadas desde CSV de muestra | Verificar contra planillas reales y relevar hojas restantes |
