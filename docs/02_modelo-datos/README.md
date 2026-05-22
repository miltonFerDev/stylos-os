# Modelo de datos

## Propósito

Documentar cómo se estructuran los datos actuales del negocio, dónde viven, qué significan y cómo se relacionan. Esto no es un diseño de base de datos, sino un mapa de la información existente.

---

## Fuentes de datos actuales

| Fuente | Tipo | Estado |
|--------|------|--------|
| Google Sheets | Hojas de cálculo | Activa |
| Fresha | Plataforma de reservas | PENDIENTE: evaluar acceso a datos |
| Cuaderno físico | Cierre diario | Activa |
| WhatsApp | Comunicaciones | Informal |
| Google Drive | Documentos | Activa |
| Meta/Instagram | Métricas de marketing | PENDIENTE: evaluar acceso |
| Web | Analíticas | PENDIENTE: evaluar acceso |

## Hojas de Google Sheets

Documentación generada durante el Sprint 2:

| Documento | Propósito |
|-----------|-----------|
| `estructura-sheets.md` | Mapeo de archivos, hojas, relaciones y clasificación (datos crudos vs. análisis) |
| `diccionario-datos.md` | Campos por hoja con tipo, obligatoriedad, descripción y validaciones sugeridas |
| `auditoria-hojas-principales.md` | Auditoría preliminar basada en CSV de muestra: anomalías detectadas, riesgos y dudas pendientes |
| `pendientes-sheets.md` | Checklist de información que falta relevar contra las planillas reales |
| `plan-validaciones-sheets.md` | Plan de validaciones futuras para Caja_diaria, Egresos y Comisiones, con priorización y dependencias |

Estos documentos se completan a medida que se relevan las planillas. Los campos y hojas no verificados están marcados como `PENDIENTE` o `TODO`.

La decisión de documentar antes de modificar está registrada en `docs/tecnico/decisiones-tecnicas/0003-documentar-sheets-antes-de-modificar.md`.

### Formato de documentación por hoja (referencia)

```
Nombre: [nombre de la hoja]
Propósito: [qué registra]
URL: [enlace]
Columnas:
  - [columna 1]: [descripción]
  - [columna 2]: [descripción]
Frecuencia de actualización: [diaria/semanal/mensual]
Responsable: [quién carga los datos]
```

## Glosario de datos

Ver `diccionario-datos.md` para la definición de cada campo del negocio.

Términos generales del glosario (PENDIENTE: completar):

- **Cierre diario**: registro de ingresos y egresos de una jornada laboral
- **Resultado operativo**: diferencia entre ingresos y egresos operativos en un período
- **Margen**: porcentaje del resultado operativo sobre los ingresos totales
- **Cuota parte**: distribución de ingresos entre los miembros del equipo según porcentaje acordado

## Relaciones entre datos

Ver `estructura-sheets.md` para el mapeo de dependencias entre archivos y hojas.

PENDIENTE: Completar el relevamiento de relaciones y dependencias contra las planillas reales.
