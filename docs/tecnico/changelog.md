# Changelog

## Propósito

Registrar los cambios relevantes del proyecto Stylos OS. No es un log de commits de Git, sino un resumen de los cambios que afectan cómo se usa o entiende el sistema.

---

## 2026-05-23

### Sprint 4 — Método de consulta gerencial (continuación)

**Documentación de fuentes y cruces de datos:**

- Catálogo de fuentes de datos (`docs/02_modelo-datos/fuentes-analisis.md`): Documenta las fuentes disponibles para análisis (Caja_diaria, Egresos, Comisiones, Cuota parte, Presupuesto, Dashboard, Fresha CSV, Hoja diaria) con nivel de confiabilidad (Alto/Medio/Parcial), limitaciones, frecuencia esperada y estado (Disponible/Parcial/Futuro). Incluye resumen tabular y sección "Qué NO son estas fuentes".

- Mapeo Fresha ↔ Sheets (`docs/02_modelo-datos/mapeo-fresha-sheets.md`): Mapeo de campos del export `report_sales-log-detail` de Fresha contra las hojas de Sheets. Campos cruzados: Fecha/Hora, Miembro del equipo, Ventas/Total, Canal, Cliente. Cruces posibles documentados (ingresos diarios, actividad de barbero, servicios) y limitaciones (sin clave común, sin desglose por medio de pago, sin cliente en Sheets). Toda relación inferida marcada como preliminar.

- Cruza de datos manual (`docs/03_procesos/cruza-datos-inicial.md`): Proceso de análisis cruzado manual entre Sheets y Fresha. Flujo de 6 pasos (definir objetivo, identificar fuentes, exportar, resumir, comparar, documentar). Cruces con prioridad hoy: ingresos diarios Fresha vs Caja_diaria, actividad de barbero Fresha vs Comisiones, resultado operativo, descuentos como análisis comercial. Cruces para después: occupancy rate, clientela nueva vs recurrente, ROI por promoción, proyección de caja. Formato de documento de análisis cruzado incluido.

**Prompts para análisis con IA:**

- Prompt consulta libre (`docs/04_prompts/prompt-consulta-libre.md`): Prompt reutilizable para recibir una pregunta libre del usuario. Estructura de 8 pasos: clasificar por área (principal + secundarias), identificar fuentes necesarias, datos disponibles, datos faltantes, análisis posible con nivel de confianza, respuesta general, recomendación condicionada, criterio de registro. Formato de respuesta estructurado con todos los niveles.

- Prompt análisis cruzado (`docs/04_prompts/prompt-analisis-cruzado.md`): Prompt reutilizable para analizar datos resumidos de varias fuentes. Estructura de 7 secciones: resumen ejecutivo, hallazgos principales, análisis cruzado (Fresha vs Sheets, actividad de equipo, resultado operativo, canales y clientes), riesgos detectados, señales tempranas, dudas y limitaciones, próximos pasos. Formato de salida completo con niveles de confianza.

**Documentación actualizada:**

- `docs/02_modelo-datos/README.md`: Agregados `fuentes-analisis.md` y `mapeo-fresha-sheets.md` al índice.
- `docs/03_procesos/README.md`: Agregado proceso de Cruza de datos al índice y descripción.
- `docs/04_prompts/README.md`: Agregados los dos prompts nuevos (consulta libre y análisis cruzado) al índice.

---

### Sprint 4 — Método de consulta gerencial (inicio)

**Decisión de diseño:**
- Consultas libres en lugar de lista cerrada — El usuario plantea la pregunta en lenguaje natural. No se impose menú ni opciones predefinidas.
- Áreas con clasificación orientativa — Cada consulta puede tener área principal y áreas secundarias (ej: consulta sobre sponsor puede involucrar marketing, inversión, caja y signos vitales).
- Cruces en tres niveles — Posibles hoy / parcialmente disponibles / deseados a futuro. No se limita el método a lo que ya está perfectamente disponible.
- Cuatro niveles de confianza — Confirmado, probable, estimado, no disponible. Con definiciones exactas.
- Registro selectivo — Solo se registra cuando afecta decisión relevante, puede repetirse, genera aprendizaje, evidencia duda recurrente, o impacta áreas clave.
- Regla central mantenida — La consulta parte del usuario. No se crean scripts, no se automatiza, no se modifica Sheets, no se propone PostgreSQL.

**Documentación creada:**

- Método de consulta gerencial (`docs/03_procesos/metodo-consulta-gerencial.md`): 8 secciones que cubren el flujo completo desde la consulta libre hasta la conversión en decisión o aprendizaje. Incluye tabla de 10 áreas con definición, mapeo de fuentes de datos por área, lista de cruces posibles en 3 niveles, guía para detectar datos faltantes, escala de confianza en 4 niveles, criterio de registro selectivo, y guía para convertir consultas en decisiones/aprendizajes.

**Documentación actualizada:**

- `docs/03_procesos/README.md`: Índice y descripción del proceso de consulta gerencial.

---

## 2026-05-22

### Sprint 2 — Completado

- Documento de auditoría preliminar de calidad de datos (`auditoria-hojas-principales.md`): análisis de Caja_diaria, Egresos y Comisiones basado en CSV de muestra. Se identificaron anomalías de formato, completitud y consistencia. Cada hallazgo se clasifica como "Hipótesis a confirmar" u "Observación preliminar".
- Pendientes de relevamiento ampliados (`pendientes-sheets.md`): se reorganizaron en secciones por hoja y tipo de duda. Se agregaron ítems específicos derivados del análisis de CSV.
- Plan de validaciones futuras (`plan-validaciones-sheets.md`): 31 validaciones definidas (10 para Caja_diaria, 12 para Egresos, 11 para Comisiones) más 5 validaciones cruzadas propuestas en estado "pendiente de confirmación". Tablas con ID, tipo, severidad y estado por validación. Priorización en 4 niveles (P1 a P4). Lista de confirmaciones previas a cualquier script.
- Corrección de caracteres residuales en `auditoria-hojas-principales.md` (texto en chino incorrectamente incluido).
- Estado actual del proyecto (`estado-actual.md`): resumen de cierre del Sprint 2 con estado de archivos, decisiones, pendientes y advertencias para la próxima sesión.

### Sprint 3 — Registro diario físico y cierre diario WhatsApp

**Hipótesis confirmadas (pre-fase):**

- Total Barbería = SUM automático de Efectivo + MPD + MPM + Tarjetas
- Celdas vacías en MPD/MPM/Tarjetas = $0
- PersonaID=7 con Servicios=0 = barbero en licencia médica con pago de comisión

**Documentación creada:**

- Proceso de cierre diario (`docs/03_procesos/cierre-diario.md`): flujo actual (as-is), problemas identificados, flujo propuesto mejorado (to-be), reglas de transición, qué no se implementa todavía. Incluye documentación de la discrepancia de Transferencia vs modelo actual de Sheets.
- Template de registro diario físico (`docs/05_templates/registro-diario-fisico.md`): formato A4 apaisado para papel/PDF, columnas (N°, Hora, Tipo, Cliente/Detalle, Barbero, Servicio, Medio de pago, Ingreso, Salida, Observación), totales al pie, lista de valores válidos para Tipo y Medio de pago, 8 ejemplos de registro, reglas de completado.
- Template de cierre WhatsApp (`docs/05_templates/cierre-diario-whatsapp.md`): formato estándar con 6 secciones obligatorias (CIERRE, COMISIONES, EGRESOS, RETIROS, TARJETAS, OBSERVACIONES), reglas de formato (montos completos, nombres consistentes, secciones con guiones si vacías), 4 ejemplos completos, relación con el registro físico.

**Templates de memoria institucional:**

- Registro de decisión (`registro-decision.md`): contexto, opciones, decisión, responsable, fecha de revisión, resultado posterior.
- Registro de consulta (`registro-consulta.md`): pregunta, contexto, fuente, respuesta, verificación, aplicación.
- Registro de aprendizaje (`registro-aprendizaje.md`): qué pasó, qué se aprendió, evidencia, impacto, fecha de revisión.
- Acta de reunión (`acta-reunion.md`): fecha y hora, lugar, participantes, temas tratados, acuerdos, pendientes.

**Documentos actualizados:**

- `diccionario-datos.md`: Total Barbería marcado como campo calculado confirmado, vacíos = $0, PersonaID=7 con observación confirmada.
- `auditoria-hojas-principales.md`: 3 hipótesis actualizadas de "pendiente" a "confirmada".
- `plan-validaciones-sheets.md`: V-CD-07, V-CD-08, V-CO-11 actualizadas a "confirmada"; lista de confirmaciones reorganizada.
- `pendientes-sheets.md`: marcar items completados.
- `docs/03_procesos/README.md`: índice actualizado con cierre diario.
- `docs/05_templates/README.md`: índice actualizado con 7 plantillas nuevas.

---

## 2026-05-21

### Agregado

- Estructura inicial del proyecto Stylos OS.
- README general.
- Documento de visión.
- SETUP para trabajo desde varias computadoras.
- Documentación técnica inicial.
- Skills locales de OpenCode para documentación, arquitectura incremental, Sheets, calidad de datos, memoria institucional y seguridad.
- Documentación de Google Sheets: estructura de archivos y hojas (`estructura-sheets.md`), diccionario de datos por hoja (`diccionario-datos.md`), pendientes de relevamiento (`pendientes-sheets.md`).
- ADR 0003: documentar Sheets antes de modificar o automatizar.
- Relevamiento estructural de Caja diaria, Egresos y Comisiones desde CSV de muestra en `data/raw/samples/`.
- Diccionario de datos actualizado con campos de Caja diaria, Egresos y Comisiones.
- Observaciones preliminares sobre cambios de formato, campos calculados y dependencias de diccionarios auxiliares.
