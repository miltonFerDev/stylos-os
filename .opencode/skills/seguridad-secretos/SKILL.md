---
name: seguridad-secretos
description: Políticas de seguridad para Stylos OS. Úsala cuando manipules .env, API keys, datos personales o cualquier información sensible. Se activa automáticamente al editar .env, .env.example o archivos con credenciales. No aplicar a documentación pública o interna no sensible.
---

# Seguridad y secretos

## Propósito

Evitar la exposición de credenciales, datos sensibles o información personal en el repositorio de Stylos OS.

## Reglas

1. **Nunca commitear secretos.** API keys, tokens, contraseñas, certificados y datos personales no deben subirse al repositorio.

2. **Usar .env para secretos.** Las variables sensibles van en `.env` (incluido en `.gitignore`). El archivo `.env.example` contiene solo valores placeholder como `PENDIENTE`.

3. **Verificar antes de committear.** Revisar que ningún archivo contenga credenciales antes de hacer un commit. Si algo sensible se subió por error, rotar la credencial inmediatamente.

4. **No almacenar documentos sensibles en el repo.** DNI, contratos firmados, claves de acceso, documentación bancaria: se referencian con su ubicación en Google Drive u otro medio seguro, no se copian al repositorio.

5. **Documentar riesgos de seguridad.** Si se identifica un riesgo de seguridad al trabajar con los datos, registrarlo en `docs/06_memoria/consultas/` o `docs/06_memoria/aprendizajes/`.

## Archivos referenciados

- `.gitignore`
- `.env.example`
- `docs/07_documentos/README.md`
- `docs/tecnico/decisiones-tecnicas/`
