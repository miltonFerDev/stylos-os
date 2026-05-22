# Estado actual — Stylos OS

## 1. Fecha de cierre de sesión

2026-05-22

## 2. Sprint actual

**Sprint 3 — Registro diario físico y cierre diario WhatsApp**

---

## 3. Qué se completó en el Sprint 3

### Pre-fase: Hipótesis confirmadas del Sprint 2

- **Total Barbería = SUM automático** — Confirmado por usuario
- **Celdas vacías en MPD/MPM/Tarjetas = $0** — Confirmado por usuario
- **PersonaID=7 con Servicios=0 = Licencia médica con pago de comisión** — Confirmado por usuario
- **Días con Total=$0** — Queda pendiente de confirmación

Documentos actualizados: `diccionario-datos.md`, `auditoria-hojas-principales.md`, `plan-validaciones-sheets.md`, `pendientes-sheets.md`.

### Documentación del flujo de cierre diario

- **Proceso de cierre diario** (`docs/03_procesos/cierre-diario.md`): Flujo actual documentado, problemas identificados, flujo propuesto mejorado, reglas de transición, qué no se implementa todavía.
- **Template de registro diario físico** (`docs/05_templates/registro-diario-fisico.md`): Formato A4 apaisado para papel/PDF, columns, valores válidos, ejemplos, instrucciones.
- **Template de cierre WhatsApp** (`docs/05_templates/cierre-diario-whatsapp.md`): Formato estándar, secciones obligatorias, reglas de formato, ejemplos completos.

### Templates de memoria institucional

- `registro-decision.md`
- `registro-consulta.md`
- `registro-aprendizaje.md`
- `acta-reunion.md`

### Documentos técnicos actualizados

- `docs/03_procesos/README.md` — Actualizado con cierre diario
- `docs/05_templates/README.md` — Actualizado con 7 plantillas nuevas

---

## 4. Archivos creados o modificados en Sprint 3

| Archivo | Acción | Fecha |
|---------|--------|-------|
| `docs/03_procesos/cierre-diario.md` | Creado | 2026-05-22 |
| `docs/05_templates/registro-diario-fisico.md` | Creado | 2026-05-22 |
| `docs/05_templates/cierre-diario-whatsapp.md` | Creado | 2026-05-22 |
| `docs/05_templates/registro-decision.md` | Creado | 2026-05-22 |
| `docs/05_templates/registro-consulta.md` | Creado | 2026-05-22 |
| `docs/05_templates/registro-aprendizaje.md` | Creado | 2026-05-22 |
| `docs/05_templates/acta-reunion.md` | Creado | 2026-05-22 |
| `docs/02_modelo-datos/diccionario-datos.md` | Actualizado (hipótesis confirmadas) | 2026-05-22 |
| `docs/02_modelo-datos/auditoria-hojas-principales.md` | Actualizado (hipótesis confirmadas) | 2026-05-22 |
| `docs/02_modelo-datos/plan-validaciones-sheets.md` | Actualizado (hipótesis confirmadas) | 2026-05-22 |
| `docs/02_modelo-datos/pendientes-sheets.md` | Actualizado | 2026-05-22 |
| `docs/03_procesos/README.md` | Actualizado | 2026-05-22 |
| `docs/05_templates/README.md` | Actualizado | 2026-05-22 |

---

## 5. Decisiones tomadas en Sprint 3

- **Template físico en A4 apaisado**: Formato horizontal para permitir más columnas sin perder legibilidad.
- **No incluir campos contables complejos**: El formato no usa "Debe/Haber" visible. Usa Ingreso/Salida que es más intuitivo para operación.
- **Transferencia como observación**: El modelo actual de Sheets no tiene columna Transferencia. Se documenta como observación para evaluación futura, sin modificar Sheets.
- **Templates de memoria liviana**: Los 4 templates de memoria institucional se crearon como base documental, sin desplazar el foco del sprint.

---

## 6. Qué NO se hizo en Sprint 3

- No se crearon scripts
- No se automatizó WhatsApp
- No se modificó Google Sheets
- No se propuso PostgreSQL ni otra base de datos
- No se cambió el modelo de datos
- No se implementó parsing automático del mensaje de cierre

---

## 7. Pendientes para Sprint 4

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

## 8. Discrepancia documentada

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

---

## 10. Comandos Git pendientes

Archivos listos para stage (pendientes de commit desde Sprint 2 y Sprint 3):

```
docs/02_modelo-datos/auditoria-hojas-principales.md
docs/02_modelo-datos/diccionario-datos.md
docs/02_modelo-datos/pendientes-sheets.md
docs/02_modelo-datos/plan-validaciones-sheets.md
docs/03_procesos/README.md
docs/03_procesos/cierre-diario.md
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