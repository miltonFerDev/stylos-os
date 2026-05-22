# Estado actual — Stylos OS

## 1. Fecha de cierre de sesión

2026-05-22

## 2. Sprint actual

**Sprint 2 — Documentación de Google Sheets actuales**

---

## 3. Qué se completó hoy

- Relevamiento de Caja_diaria, Egresos y Comisiones desde CSV de muestra en `data/raw/samples/`
- Auditoría preliminar de calidad de datos (`auditoria-hojas-principales.md`): 3 hojas analizadas, anomalías detectadas y clasificadas
- Plan de validaciones futuras (`plan-validaciones-sheets.md`): 31 validaciones definidas + 5 cruzadas propuestas en estado "pendiente de confirmación"
- Pendientes de relevamiento reorganizados por hoja y tipo (`pendientes-sheets.md`)
- Corrección de caracteres residuales en `auditoria-hojas-principales.md`
- Actualización de `README.md` con los documentos del Sprint 2

---

## 4. Archivos creados o modificados

| Archivo | Acción | Fecha |
|---------|--------|-------|
| `docs/02_modelo-datos/estructura-sheets.md` | Creado | 2026-05-21 |
| `docs/02_modelo-datos/diccionario-datos.md` | Creado | 2026-05-21 |
| `docs/02_modelo-datos/pendientes-sheets.md` | Creado | 2026-05-21, ampliado | 2026-05-22 |
| `docs/02_modelo-datos/auditoria-hojas-principales.md` | Creado | 2026-05-22, corregido | 2026-05-22 |
| `docs/02_modelo-datos/plan-validaciones-sheets.md` | Creado | 2026-05-22 |
| `docs/02_modelo-datos/README.md` | Actualizado | 2026-05-22 |
| `docs/tecnico/decisiones-tecnicas/0003-documentar-sheets-antes-de-modificar.md` | Creado | 2026-05-21 |
| `docs/tecnico/changelog.md` | Actualizado | 2026-05-21, 2026-05-22 |
| `docs/tecnico/estado-actual.md` | Creado | 2026-05-22 |

---

## 5. Decisiones tomadas

- **ADR 0003**: Documentar Sheets antes de modificar o automatizar. No se toca ninguna planilla ni se crean scripts hasta completar la documentación.
- Todo hallazgo inferido desde CSV se marca como "Hipótesis a confirmar" u "Observación preliminar". No se trata como certeza.
- **PersonaID=7 en Comisiones**: Se redactó como "pago fijo, ajuste, retiro u otro concepto no estrictamente comisional". No se asumió alquiler.
- **Celdas vacías en medios de pago**: No se asume que vacía = $0. Se requiere confirmación del usuario.
- **Validaciones cruzadas V-CR-01 a V-CR-05**: Se documentan como "pendiente de confirmación" en sección separada. No se treatan como reglas válidas todavía.
- **Formato CSV vs Sheets**: Los CSV analizados pueden no reflejar fórmulas reales ni formatos de celda aplicados en el archivo original.

---

## 6. Qué NO se hizo todavía

- No se crearon scripts de ningún tipo
- No se modificaron Google Sheets (ni validaciones, ni formato, ni estructura)
- No se automatizó nada
- No se propuso PostgreSQL ni ninguna otra base de datos
- No se relevaron las 11 hojas restantes del diccionario de datos (Cuota parte, Presupuesto, Dashboard, Personas, Categorías, Subcategorías, Medios de pago, Eventos, Decisiones, Consultas IA, Aprendizajes)
- No se verificaron fórmulas reales en Sheets (Total Barbería, Total_Ventas, Total_Abonado)
- No se confirmaron hipótesis contra las planillas reales
- No se diseñó el registro diario físico
- No se estandarizó el mensaje de cierre diario por WhatsApp
- No se crearon las plantillas de memoria institucional

---

## 7. Pendientes inmediatos

### Confirmaciones con el usuario

- [ ] ¿Los días con Total = $0 en Caja_diaria son días no trabajados o errores de carga?
- [ ] ¿Las celdas vacías en MPD, MPM y Tarjetas significan $0 o carga omitida?
- [ ] ¿Cuál es la fórmula de Total Barbería: SUM de columnas o valor manual?
- [ ] ¿Cuál es la fórmula de Total_Ventas y Total_Abonado?
- [ ] ¿Cuándo es obligatorio PersonaID en Egresos?
- [ ] ¿Cuándo es obligatorio MedioPagoID en Egresos?
- [ ] ¿Qué representa PersonaID=7 con Servicios=0 y Comisión fija ($43.000/$64.500)?
- [ ] ¿Qué significa Servicios = 0 en Comisiones?

### Relevamientos pendientes

- [ ] Hojas diccionario: Personas, Categorías, Subcategorías, Medios de pago
- [ ] Las 11 hojas restantes del diccionario de datos
- [ ] Fórmulas reales en Sheets (verificar contra archivo real)
- [ ] URLs exactas de cada archivo de Sheets
- [ ] Frecuencia real de modificación de cada hoja

---

## 8. Próximo paso recomendado

**Sprint 3 — Registro diario físico y cierre diario WhatsApp**

1. Diseñar el registro diario físico (plantilla en papel o PDF)
2. Estandarizar el mensaje de cierre diario por WhatsApp
3. Crear plantillas de memoria institucional

Antes de iniciar el Sprint 3, confirmar al menos las primeras 3-4 hipótesis con el usuario para no avanzar con suposiciones incorrectas.

---

## 9. Comandos Git ejecutados o pendientes

**Estado**: Git no está disponible en el entorno actual. Los archivos están listos para stage y commit desde una terminal con Git instalado.

**Archivos en staging** (pendientes de commit):

```
docs/02_modelo-datos/README.md
docs/02_modelo-datos/auditoria-hojas-principales.md
docs/02_modelo-datos/diccionario-datos.md
docs/02_modelo-datos/estructura-sheets.md
docs/02_modelo-datos/pendientes-sheets.md
docs/02_modelo-datos/plan-validaciones-sheets.md
docs/tecnico/decisiones-tecnicas/0003-documentar-sheets-antes-de-modificar.md
docs/tecnico/changelog.md
docs/tecnico/estado-actual.md
```

**Comando para ejecutar en terminal con Git**:

```bash
git add docs/02_modelo-datos/README.md \
        docs/02_modelo-datos/auditoria-hojas-principales.md \
        docs/02_modelo-datos/diccionario-datos.md \
        docs/02_modelo-datos/estructura-sheets.md \
        docs/02_modelo-datos/pendientes-sheets.md \
        docs/02_modelo-datos/plan-validaciones-sheets.md \
        docs/tecnico/decisiones-tecnicas/0003-documentar-sheets-antes-de-modificar.md \
        docs/tecnico/changelog.md \
        docs/tecnico/estado-actual.md
```

---

## 10. Advertencias importantes para la próxima sesión

- **Ningún hallazgo del CSV es una certeza.** Todo requiere verificación contra las planillas reales de Google Sheets antes de convertirse en reglas o validaciones.
- **Las validaciones cruzadas V-CR-01 a V-CR-05 NO son reglas definidas.** Son propuestas pendientes de confirmación. No implementarlas sin antes confirmar las relaciones entre hojas.
- **Los campos marcados como "posible campo calculado" requieren verificación de fórmula en Sheets.** Pueden ser valores cargados manualmente.
- **ADR 0003 sigue vigente.** No modificar Sheets ni crear scripts hasta completar la fase de documentación.
- **Los diccionarios auxiliares (Personas, Categorías, Subcategorías, Medios de pago) no están relevados.** Toda validación que dependa de ellos (nivel P3) está bloqueada hasta obtener esa información.
- **Cambio de formato ~ene 2026:** Los IDs cambiaron de numéricos a UUID y los valores monetarios perdieron el prefijo `$`. Puede afectar cualquier script futuro que asuma formato numérico uniforme.
- **PersonaID vacío en Egresos y Comisiones:** Un alto porcentaje de registros no tienen PersonaID. Esto afecta la capacidad de atribuir gastos y comisiones. Priorizar confirmación con el usuario.
- **Sprint 3 no debe iniciar sin confirmar al menos las primeras hipótesis.** Si se diseña el registro diario físico sobre suposiciones incorrectas, el cierre diario de WhatsApp tambiénwill be based on flawed assumptions.