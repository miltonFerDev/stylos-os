---
name: calidad-datos
description: Validación y consistencia de datos en Stylos OS. Úsala cuando analices datos exportados, verifiques cargas, o documentes reglas de validación. No aplicar cuando se trabaje solo con documentación o criterios sin datos.
---

# Calidad de datos

## Propósito

Detectar, documentar y corregir problemas de calidad en los datos económicos, operativos y comerciales de Stylo's Barber.

## Reglas

1. **Verificar consistencia.** Al analizar datos exportados, comprobar: valores nulos o vacíos, duplicados, rangos fuera de lo esperado, tipos de dato incorrectos.

2. **Documentar reglas de validación.** Cada hoja de Sheets debe tener sus reglas de validación documentadas en el archivo correspondiente de `docs/02_modelo-datos/`.

3. **No corregir datos en Sheets automáticamente.** Los errores se reportan, no se corrigen desde scripts o skills. La corrección la hace una persona.

4. **Registrar problemas encontrados.** Usar `docs/06_memoria/aprendizajes/` o `docs/06_memoria/consultas/` para dejar registro de problemas de datos recurrentes y cómo se resolvieron.

5. **Distinguir datos crudos de procesados.** En `data/raw/` solo datos exportados sin modificar. En `data/processed/` datos limpios o transformados, con documentación de los cambios aplicados.

## Archivos referenciados

- `docs/02_modelo-datos/README.md`
- `data/raw/`
- `data/processed/`
- `docs/06_memoria/aprendizajes/`
- `docs/06_memoria/consultas/`
