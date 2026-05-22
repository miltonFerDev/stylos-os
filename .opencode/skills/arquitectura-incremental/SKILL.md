---
name: arquitectura-incremental
description: Principio de arquitectura gradual para Stylos OS. Úsala SOLO cuando se proponga agregar herramientas, dependencias, Docker, bases de datos o automatizaciones. No aplicar cuando se trate de documentación, criterios o memoria institucional.
---

# Arquitectura incremental

## Propósito

Evitar sobreingeniería en Stylos OS asegurando que cada avance técnico responde a una necesidad real del negocio y no a entusiasmo técnico.

## Reglas

1. **No construir infraestructura antes de tiempo.** No agregar PostgreSQL, Docker, n8n, Metabase, IA local, app propia ni ninguna herramienta avanzada hasta que exista una necesidad concreta y documentada.

2. **Toda nuevo componente debe justificarse.** Antes de agregar cualquier herramienta o dependencia, responder: ¿Qué problema del negocio resuelve? ¿Por qué no alcanza con lo actual? ¿Quién lo va a mantener?

3. **Preferir la herramienta más simple que funcione.** Si un problema se resuelve con una hoja de cálculo y un Markdown, no hace falta más.

4. **Documentar la decisión.** Si se agrega una herramienta, registrar en `docs/tecnico/decisiones-tecnicas/` el contexto, las alternativas consideradas y la justificación.

## Orden de avance sugerido

El orden correcto siempre es:

1. Documentación y criterios
2. Registro de datos y memoria
3. Análisis manual con IA
4. Recién después: scripts simples
5. Recién después: automatizaciones
6. Recién al final: infraestructura compleja

## Archivos referenciados

- `docs/tecnico/arquitectura.md`
- `docs/tecnico/decisiones-tecnicas/`
- `docs/00_vision/vision-stylos-os.md` (secciones 9 y 13)
