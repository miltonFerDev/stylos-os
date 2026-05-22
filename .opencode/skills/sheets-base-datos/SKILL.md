---
name: sheets-base-datos
description: Google Sheets como fuente de datos principal de Stylos OS. Úsala cuando documentes hojas de cálculo, modeles datos, o analices información proveniente de Google Sheets.
---

# Sheets como base de datos

## Propósito

Documentar y mantener el modelo de datos actual de Stylos OS, donde Google Sheets es la fuente principal de información económica, operativa y comercial del negocio.

## Reglas

1. **Documentar cada hoja.** En `docs/02_modelo-datos/`, crear un archivo por cada hoja de Sheets con: nombre, propósito, URL, columnas principales y frecuencia de actualización.

2. **No modificar las hojas originales desde skills o scripts.** En esta fase, solo se documenta y analiza. Las modificaciones a Sheets se hacen manualmente.

3. **Mantener un glosario de datos.** En `docs/02_modelo-datos/README.md`, definir los términos clave usados en los datos del negocio (ej: "cierre diario", "resultado operativo", "margen").

4. **Documentar relaciones entre hojas.** Si los datos de una hoja dependen de otra, registrarlo.

5. **Marcar lo que falta como PENDIENTE.** Si una hoja no está documentada o una columna no está clara, dejarlo explícito con `PENDIENTE`.

## Archivos referenciados

- `docs/02_modelo-datos/README.md`
- `docs/02_modelo-datos/` (archivos por hoja)
- `data/raw/` (exportaciones sin procesar)
- `data/processed/` (datos procesados)
