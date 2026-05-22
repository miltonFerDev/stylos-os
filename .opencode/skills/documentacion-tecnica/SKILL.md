---
name: documentacion-tecnica
description: Reglas de documentación técnica obligatoria para Stylos OS. Úsala cuando crees o modifiques scripts, decidas cambios de arquitectura, o edites archivos en docs/tecnico/. No aplica a documentación de negocio (criterios, procesos, memoria).
---

# Documentación técnica

## Propósito

Garantizar que todo cambio técnico en Stylos OS quede documentado para que otra persona con conocimiento pueda entenderlo, mantenerlo o corregirlo.

## Reglas obligatorias

1. **Todo script debe documentarse.** Cualquier script en `scripts/` o `docs/tecnico/scripts/` debe incluir un comentario al inicio con: propósito, dependencias, uso esperado y autor.

2. **Toda decisión técnica debe registrarse.** Usar `docs/tecnico/decisiones-tecnicas/` con el formato `YYYY-MM-DD-titulo-breve.md`. Incluir contexto, opciones consideradas, decisión tomada y justificación.

3. **La arquitectura se actualiza con cada cambio.** Si un cambio afecta cómo se relacionan los componentes del sistema, actualizar `docs/tecnico/arquitectura.md`.

4. **El changelog se actualiza con cada cambio relevante.** Usar `docs/tecnico/changelog.md`. Una entrada por cambio, no por commit.

## Archivos referenciados

- `docs/tecnico/arquitectura.md` — descripción de la arquitectura actual y evolución prevista
- `docs/tecnico/instalacion.md` — instrucciones de instalación
- `docs/tecnico/changelog.md` — registro de cambios relevantes
- `docs/tecnico/scripts/` — scripts técnicos documentados
- `docs/tecnico/decisiones-tecnicas/` — decisiones técnicas registradas
- `docs/01_criterios/` — criterios de negocio que puedan afectar decisiones técnicas
