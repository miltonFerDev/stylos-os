# Estado actual — Stylos OS

## 1. Fecha de cierre de sesión

2026-05-23

## 2. Sprint actual

**Sprint 4 — Método de consulta gerencial**

---

## 3. Qué se completó en el Sprint 4

### Fase 1: Método de consulta gerencial

- **Documento de método de consulta gerencial** (`docs/03_procesos/metodo-consulta-gerencial.md`): 8 secciones que cubren el flujo completo desde la consulta libre hasta la conversión en decisión o aprendizaje. Incluye:
  - Recibir consulta libre: principio de que el usuario formula sin menú predefinido.
  - Clasificar por área: tabla de 10 áreas con definición, clasificación orientativa con área principal y secundarias (ejemplo incluido aclarado como ilustrativo).
  - Identificar fuentes de datos: mapeo área → fuentes, referencias a estructura-sheets y diccionario-datos, lista de fuentes pendientes.
  - Cruces posibles en 3 niveles: hoy (verificados), parcialmente (disponibles con limitaciones), deseados a futuro (requieren datos no relevados).
  - Datos faltantes: cómo detectar qué falta, pasos ante limitaciones, lista de hojas con TODO.
  - Nivel de confianza: escala de 4 niveles (confirmado, probable, estimado, no disponible) con definición exacta y guía de comunicación.
  - Registro selectivo: criterio de cuándo registrar (decisión relevante, repetición, aprendizaje, duda recurrente, impacto en áreas clave) y cuándo descartar.
  - Convertir en decisión o aprendizaje: criterio para derivar consultas a memoria institucional.
  - Sección "Qué NO hace este método" con reglas explícitas.

### Fase 2: Fuentes y cruces de datos

- **Catálogo de fuentes** (`docs/02_modelo-datos/fuentes-analisis.md`): 16 fuentes documentadas (Sheets, Fresha, hoja diaria) con nivel de confiabilidad, limitaciones, frecuencia esperada y estado. Tabla resumen. Sección "Qué NO son estas fuentes" con reglas explícitas.

- **Mapeo Fresha ↔ Sheets** (`docs/02_modelo-datos/mapeo-fresha-sheets.md`): Campos del export `report_sales-log-detail` mapeados contra Sheets. Relaciones inferidas marcadas como preliminares. Qué se puede cruzar (ingresos diarios, actividad de barbero, servicios) y qué no (canal, cliente, artículo, descuentos). Limitaciones documentadas.

- **Cruza de datos manual** (`docs/03_procesos/cruza-datos-inicial.md`): Flujo de 6 pasos para análisis cruzado manual. 4 cruces con prioridad hoy (Fresha vs Caja_diaria, Fresha vs Comisiones, resultado operativo, descuentos). 4 cruces para después (occupancy rate, clientela nueva vs recurrente, ROI promoción, proyección de caja). Formato de documento de análisis incluido.

### Fase 3: Prompts para análisis con IA

- **Prompt consulta libre** (`docs/04_prompts/prompt-consulta-libre.md`): Estructura de 8 pasos con formato de respuesta estructurado. Clasificar por área principal/secundarias, identificar fuentes, datos disponibles, datos faltantes, análisis con nivel de confianza, respuesta general, recomendación condicionada, criterio de registro.

- **Prompt análisis cruzado** (`docs/04_prompts/prompt-analisis-cruzado.md`): Estructura de 7 secciones con formato de salida completo. Resumen ejecutivo, hallazgos principales, análisis cruzado, riesgos, señales tempranas, dudas y limitaciones, próximos pasos.

### Documentos actualizados

- `docs/02_modelo-datos/README.md`: Agregados `fuentes-analisis.md` y `mapeo-fresha-sheets.md` al índice.
- `docs/03_procesos/README.md`: Índice y descripción de Cruza de datos agregados.
- `docs/04_prompts/README.md`: Índice actualizado con los dos prompts nuevos.

---

## 4. Archivos creados o modificados en Sprint 4

| Archivo | Acción | Fecha |
|---------|--------|-------|
| `docs/03_procesos/metodo-consulta-gerencial.md` | Creado | 2026-05-23 |
| `docs/02_modelo-datos/fuentes-analisis.md` | Creado | 2026-05-23 |
| `docs/02_modelo-datos/mapeo-fresha-sheets.md` | Creado | 2026-05-23 |
| `docs/03_procesos/cruza-datos-inicial.md` | Creado | 2026-05-23 |
| `docs/04_prompts/prompt-consulta-libre.md` | Creado | 2026-05-23 |
| `docs/04_prompts/prompt-analisis-cruzado.md` | Creado | 2026-05-23 |
| `docs/02_modelo-datos/README.md` | Actualizado | 2026-05-23 |
| `docs/03_procesos/README.md` | Actualizado | 2026-05-23 |
| `docs/04_prompts/README.md` | Actualizado | 2026-05-23 |
| `docs/tecnico/changelog.md` | Actualizado | 2026-05-23 |
| `docs/tecnico/estado-actual.md` | Actualizado | 2026-05-23 |

---

## 5. Decisiones tomadas en Sprint 4

- **Consulta libre sin lista cerrada**: El usuario formula en lenguaje natural. No se presenta menú ni opciones predefinidas. Los ejemplos se marcan explícitamente como ilustrativos, no como menú.
- **Áreas con clasificación orientativa**: Cada consulta puede tener área principal y áreas secundarias. Una consulta sobre sponsor puede involucrar marketing, inversión, caja y signos vitales simultáneamente.
- **Cruces en tres niveles**: Se documentan cruces posibles hoy (verificados), parcialmente disponibles, y deseados a futuro. No se limita el método a lo que ya está perfectamente disponible.
- **Nivel de confianza explícito**: Toda respuesta incluye su nivel (confirmado, probable, estimado, no disponible). No se infla la confianza. La honestidad sobre la calidad del dato es prioritaria.
- **Registro selectivo**: No toda consulta se registra. Solo cuando afecta decisión relevante, puede repetirse, genera aprendizaje, evidencia duda recurrente, o impacta áreas clave (finanzas, operación, marketing, equipo, estrategia).
- **Conversión a decisión o aprendizaje**: Si la consulta produce un cambio de criterio, una acción tomada, o una lección validada, se deriva a memoria institucional.
- **Fresha como fuente de detalle, Sheets como fuente de consolidado**: Fresha aporta detalle por servicio, cliente y canal. Sheets aporta totales consolidados diarios y mensuales. Se cruzan solo cuando es validado.
- **Relaciones Fresha ↔ Sheets como preliminares**: Toda inferencia de mapeo entre Fresha y Sheets se marca como "preliminar" hasta validarse contra planillas reales.
- **Cruces en niveles de disponibilidad**: Se separan cruces posibles hoy, parcialmente disponibles, y deseados a futuro. El método no limita el análisis a lo que ya funciona perfectamente.

---

## 6. Qué NO se hizo en Sprint 4

- No se creó lista cerrada de consultas objetivo
- No se crearon scripts
- No se automatizó ninguna parte del proceso de consulta ni exportación
- No se modificó Google Sheets
- No se propuso PostgreSQL ni otra base de datos
- No se condicionó al usuario a formulaciones predefinidas
- No se creó dashboard
- No se implementó conexión automática entre Fresha y Sheets
- No se validó el mapeo Fresha ↔ Sheets contra planillas reales (es preliminar)

---

## 7. Pendientes para Sprint 5

### Confirmaciones pendientes del Sprint 2

- [ ] Días con Total=$0: ¿días no trabajados o errores de carga?
- [ ] Fórmula de Total_Ventas y Total_Abonado
- [ ] Cuándo es obligatorio PersonaID en Egresos
- [ ] Cuándo es obligatorio MedioPagoID en Egresos
- [ ] Contenido de hojas diccionario (Personas, Categorías, Subcategorías, Medios de pago)

### Documentación pendiente

- [ ] Proceso de carga de ingresos (de Fresha/cuaderno a Sheets)
- [ ] Proceso de registro de egresos
- [ ] Proceso de pago de comisiones
- [ ] Proceso de pago de sueldos
- [ ] Template de evaluación de sponsor
- [ ] Template de evaluación de promoción
- [ ] Template de informe semanal
- [ ] Template de informe mensual

### Relevamientos pendientes

- [ ] URLs exactas de cada archivo de Sheets
- [ ] Verificar fórmulas reales contra planillas reales
- [ ] Relevar hojas restantes del diccionario (Cuota parte, Presupuesto, Dashboard, Personas, Categorías, Subcategorías, Medios de pago, Eventos)

---

## 8. Discrepancia documentada (Sprint 3)

**Transferencia como medio de pago operativo**

El template de registro físico incluye Transferencia como medio de pago posible. Sin embargo, el modelo actual de datos en Sheets (hoja Caja_diaria) solo contempla Efectivo, MPD, MPM y Tarjetas.

**No se.modificó el modelo de datos en este sprint.** Esta discrepancia se documenta como observación para evaluación futura. Si se registra una transferencia en el formato físico, se debe aclarar en la columna Observación y en el mensaje de WhatsApp, sin agruparla bajo otro medio.

---

## 9. Advertencias para la próxima sesión

- **ADR 0003 sigue vigente.** No modificar Sheets ni crear scripts hasta completar la fase de documentación.
- **Las 3 hipótesis confirmadas ya no son hipótesis.** Se treatan como reglas confirmadas.
- **Días con Total=$0 sigue pendiente de confirmación.** No implementar validaciones basadas en ese dato hasta confirmarlo.
- **El mensaje de cierre WhatsApp se arma manualmente.** No implementar scripts de parsing automático hasta que el formato esté en uso y validado.
- **Fresha no se reemplaza.** El registro físico es un control de caja y respaldo operativo, no un CRM.
- **Consulta gerencial sin menú cerrado.** No imponer listas de consultas predefinidas. Los ejemplos son ilustrativos, no opciones de un menú.
- **Nivel de confianza explícito.** Toda respuesta a consulta debe incluir su nivel. No inflar la confianza.
- **Mapeo Fresha ↔ Sheets es preliminar.** No usar como fuente de verdad hasta validar contra planillas reales.
- **Prompts en uso.** Los prompts de consulta libre y análisis cruzado son la base para interactuar con IA sobre datos del negocio.

---

## 10. Comandos Git pendientes

Archivos listos para stage (pendientes de commit desde Sprint 2, Sprint 3 y Sprint 4):

```
docs/02_modelo-datos/auditoria-hojas-principales.md
docs/02_modelo-datos/diccionario-datos.md
docs/02_modelo-datos/fuentes-analisis.md
docs/02_modelo-datos/mapeo-fresha-sheets.md
docs/02_modelo-datos/pendientes-sheets.md
docs/02_modelo-datos/plan-validaciones-sheets.md
docs/03_procesos/README.md
docs/03_procesos/cierre-diario.md
docs/03_procesos/cruza-datos-inicial.md
docs/03_procesos/metodo-consulta-gerencial.md
docs/04_prompts/README.md
docs/04_prompts/prompt-analisis-cruzado.md
docs/04_prompts/prompt-consulta-libre.md
docs/05_templates/README.md
docs/05_templates/registro-diario-fisico.md
docs/05_templates/cierre-diario-whatsapp.md
docs/05_templates/registro-decision.md
docs/05_templates/registro-consulta.md
docs/05_templates/registro-aprendizaje.md
docs/05_templates/acta-reunion.md
docs/tecnico/changelog.md
docs/tecnico/estado-actual.md
```