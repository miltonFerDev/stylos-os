# Setup de Stylos OS

## Propósito

Guía para configurar el entorno de trabajo de Stylos OS en una máquina local.

## Requisitos

- Git
- Un editor de texto (recomendado: VS Code)
- Acceso a Google Sheets (fuente principal de datos)
- Acceso a Google Drive (documentos compartidos)

## Pasos

### 1. Clonar el repositorio

```bash
git clone <url-del-repositorio>
cd stylos-os
```

### 2. Configurar variables de entorno

Copiar `.env.example` a `.env` y completar los valores necesarios:

```bash
cp .env.example .env
```

### 3. Estructura de carpetas

La estructura ya está creada. Ver `README.md` para el detalle completo.

### 4. Google Sheets

Las hojas de cálculo siguen siendo la fuente principal de datos. Los IDs y nombres de las hojas relevantes deben documentarse en `docs/02_modelo-datos/`.

PENDIENTE: Documentar IDs y URLs de las hojas de Google Sheets utilizadas.

### 5. Convenciones de trabajo

- Los documentos se escriben en Markdown.
- Cada archivo Markdown debe tener título, propósito y secciones iniciales.
- La información faltante se marca como `PENDIENTE` o `TODO`.
- No se commitean datos sensibles ni credenciales.
- Los datos crudos van en `data/raw/`, los procesados en `data/processed/`.
- Los backups manuales van en `backups/`.

## Verificación

PENDIENTE: Definir checklist de verificación tras la configuración inicial.
