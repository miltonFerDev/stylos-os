# Changelog

## Propósito

Registrar los cambios relevantes del proyecto Stylos OS. No es un log de commits de Git, sino un resumen de los cambios que afectan cómo se usa o entiende el sistema.

---

## 2026-05-22

### Agregado

- Documento de auditoría preliminar de calidad de datos (`auditoria-hojas-principales.md`): análisis de Caja_diaria, Egresos y Comisiones basado en CSV de muestra. Se identificaron anomalías de formato, completitud y consistencia. Cada hallazgo se clasifica como "Hipótesis a confirmar" u "Observación preliminar".
- Pendientes de relevamiento ampliados (`pendientes-sheets.md`): se reorganizaron en secciones por hoja y tipo de duda. Se agregaron ítems específicos derivados del análisis de CSV.

### Pendiente

- Diseñar registro diario físico.
- Estandarizar mensaje de cierre diario.
- Crear plantillas de memoria institucional.

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

### Pendiente

- Diseñar registro diario físico.
- Estandarizar mensaje de cierre diario.
- Crear plantillas de memoria institucional.
