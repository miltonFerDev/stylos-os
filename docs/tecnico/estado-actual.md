# Estado actual — Stylos OS

## 1. Fecha de cierre de sesión

2026-05-23

## 2. Sprint actual

**Sprint 4 — Método de consulta gerencial**

---

## 3. Qué se completó en el Sprint 4

### Método de consulta gerencial

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

- **Regla central**: La consulta parte del usuario. Sin lista cerrada, sin scripts, sin automatización, sin modificar Sheets, sin proponer PostgreSQL.

### Documentos actualizados

- `docs/03_procesos/README.md`: Índice y descripción del proceso de consulta gerencial agregado.

---

## 4. Archivos creados o modificados en Sprint 4

| Archivo | Acción | Fecha |
|---------|--------|-------|
| `docs/03_procesos/metodo-consulta-gerencial.md` | Creado | 2026-05-23 |
| `docs/03_procesos/README.md` | Actualizado (índice y descripción) | 2026-05-23 |
| `docs/tecnico/changelog.md` | Actualizado (entrada Sprint 4) | 2026-05-23 |
| `docs/tecnico/estado-actual.md` | Actualizado (cierre Sprint 4) | 2026-05-23 |

---

## 5. Decisiones tomadas en Sprint 4

- **Consulta libre sin lista cerrada**: El usuario formula en lenguaje natural. No se presenta menú ni opciones predefinidas. Los ejemplos se marcan explícitamente como ilustrativos, no como menú.
- **Áreas con clasificación orientativa**: Cada consulta puede tener área principal y áreas secundarias. Una consulta sobre sponsor puede involucrar marketing, inversión, caja y signos vitales simultáneamente.
- **Cruces en tres niveles**: Se documentan cruces posibles hoy (verificados), parcialmente disponibles, y deseados a futuro. No se limita el método a lo que ya está perfectamente disponible.
- **Nivel de confianza explícito**: Toda respuesta incluye su nivel (confirmado, probable, estimado, no disponible). No se infla la confianza. La honestidad sobre la calidad del dato es prioritaria.
- **Registro selectivo**: No toda consulta se registra. Solo cuando afecta decisión relevante, puede repetirse, genera aprendizaje, evidencia duda recurrente, o impacta áreas clave (finanzas, operación, marketing, equipo, estrategia).
- **Conversión a decisión o aprendizaje**: Si la consulta produce un cambio de criterio, una acción tomada, o una lección validada, se deriva a memoria institucional.

---

## 6. Qué NO se hizo en Sprint 4

- No se creó lista cerrada de consultas objetivo
- No se crearon scripts
- No se automatizó ninguna parte del proceso de consulta
- No se modificó Google Sheets
- No se propuso PostgreSQL ni otra base de datos
- No se condicionó al usuario a formulaciones predefinidas

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

---

## 10. Comandos Git pendientes

Archivos listos para stage (pendientes de commit desde Sprint 2, Sprint 3 y Sprint 4):

```
docs/02_modelo-datos/auditoria-hojas-principales.md
docs/02_modelo-datos/diccionario-datos.md
docs/02_modelo-datos/pendientes-sheets.md
docs/02_modelo-datos/plan-validaciones-sheets.md
docs/03_procesos/README.md
docs/03_procesos/cierre-diario.md
docs/03_procesos/metodo-consulta-gerencial.md
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