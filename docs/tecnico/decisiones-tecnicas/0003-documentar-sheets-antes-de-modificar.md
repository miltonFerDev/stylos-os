# ADR 0003: Documentar Google Sheets antes de modificar o automatizar

## Fecha

2026-05-21

## Contexto

Stylos OS se encuentra en fase inicial de documentación. Los datos principales del negocio viven en Google Sheets en tres archivos conocidos: `Stylos_Data`, `Stylos_Analisis` y `Stylos_Presupuesto`.

Actualmente no existe documentación formal sobre:

- La estructura exacta de cada archivo y hoja
- Las columnas y tipos de dato de cada tabla
- Las fórmulas críticas que producen los indicadores del negocio
- Las dependencias entre hojas y archivos
- Las validaciones existentes o faltantes

Sin este conocimiento documentado, cualquier modificación o automatización corre el riesgo de:

- Romper fórmulas sin saberlo
- Perder datos por malinterpretar la estructura
- Automatizar procesos que ya están mal diseñados
- Dificultar la futura migración a un sistema más robusto

## Decisión

Primero documentar exhaustivamente las planillas de Google Sheets antes de realizar cualquier modificación, automatización o migración.

Esto implica:

1. Completar `docs/02_modelo-datos/estructura-sheets.md` con el mapeo de archivos y hojas
2. Completar `docs/02_modelo-datos/diccionario-datos.md` con todas las columnas reales
3. Relevar y documentar dependencias, fórmulas críticas y validaciones actuales
4. Marcar como PENDIENTE todo lo que no se pueda verificar directamente

Queda prohibido en esta fase:

- Modificar la estructura de las planillas (agregar/eliminar columnas u hojas)
- Cambiar fórmulas existentes
- Crear scripts que modifiquen datos en Sheets
- Migrar datos a otra plataforma
- Agregar automatizaciones que escriban en Sheets

## Justificación

- **Principio central del proyecto:** "Primero utilidad de gestión. Después tecnología." Documentar es anterior a modificar o automatizar.
- **Skill arquitectura-incremental:** No construir infraestructura antes de tiempo. Primero entender lo que existe.
- **Riesgo:** Sin documentación, cualquier cambio puede tener consecuencias imprevistas en fórmulas y dependencias que no conocemos.
- **Costo:** Documentar solo requiere acceso de lectura a las planillas y tiempo de relevamiento. No requiere herramientas, scripts ni autorización especial.
- **Trazabilidad:** Una vez documentado, cualquier cambio futuro queda registrado contra una línea de base clara.

## Consecuencias

### Positivas

- Se crea una línea de base documentada del estado actual de los datos
- Se reduce el riesgo de romper algo al modificar
- Se facilita la detección de problemas de calidad de datos
- Se construye el conocimiento necesario para futuras decisiones técnicas
- Cualquier persona nueva puede entender el sistema de datos sin acceso directo a Sheets

### Negativas

- Retrasa cualquier mejora o automatización hasta completar el relevamiento
- Requiere tiempo de relevamiento manual que podría usarse en otras tareas
- Puede generar documentación extensa que después requiera mantenimiento

## Estado

Aprobada.

## Próxima revisión

Al completar el relevamiento de todas las hojas y columnas documentadas en `docs/02_modelo-datos/pendientes-sheets.md`.
