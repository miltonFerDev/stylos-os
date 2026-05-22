# Stylos OS

Sistema interno de gestión e inteligencia para Stylo's Barber, Ituzaingó, Argentina.

---

## 1. Qué es Stylos OS

Stylos OS es la memoria de gestión de Stylo's Barber: un sistema gradual para ordenar datos, documentos, decisiones y aprendizajes, con el objetivo de tomar mejores decisiones económicas, comerciales y operativas.

No nace como una app ni como una automatización aislada. Nace como una **memoria institucional y analítica** pensada para servir tanto a la estructura actual del negocio como a una posible futura cooperativa.

---

## 2. Objetivo del proyecto

Stylos OS busca ayudar a responder preguntas concretas de gestión:

- ¿Cuánto ganó realmente el negocio?
- ¿Qué cambió respecto al mes anterior?
- ¿Qué gastos se desordenaron?
- ¿Podemos asumir un costo nuevo?
- ¿Conviene hacer una promoción, sponsor o alianza?
- ¿Qué datos explican una baja o suba de clientes?
- ¿Qué aprendimos de decisiones anteriores?
- ¿Qué documento o criterio respalda una decisión?

El objetivo principal no es automatizar todo, sino **mejorar la calidad de decisión**.

---

## 3. Principio central

**Primero utilidad de gestión. Después tecnología.**

Cada avance del sistema debe justificar su existencia porque mejora al menos uno de estos puntos:

- Reduce errores
- Ahorra tiempo administrativo
- Mejora una decisión
- Ordena un proceso
- Aclara un dato
- Deja trazabilidad
- Permite aprender de lo hecho
- Facilita una futura estructura cooperativa

Si una herramienta, script, dashboard o automatización no mejora alguno de estos puntos, no debe priorizarse.

---

## 4. Estado actual del proyecto

El proyecto se encuentra en **fase inicial**.

- La fuente principal de datos sigue siendo **Google Sheets**
- Los documentos se organizan en **Markdown y Google Drive**
- No existe app propia, automatizaciones, base de datos externa ni IA integrada
- La prioridad es documentar la visión, ordenar la información existente y crear memoria institucional

Las automatizaciones, bases de datos externas, dashboards y app propia quedan para fases posteriores, cuando exista una necesidad real que lo justifique.

---

## 5. Qué incluye Stylos OS

Stylos OS agrupa progresivamente las siguientes áreas:

### Datos económicos

Ingresos diarios, egresos, comisiones, sueldos, retiros, presupuesto, fondos, resultado operativo, margen, caja proyectada.

### Datos operativos

Servicios, barberos, medios de pago, cierres diarios, eventos del negocio, datos provenientes de Fresha cuando estén disponibles.

### Datos comerciales y de marketing

Campañas, promociones, sponsors, alianzas, métricas de Instagram, métricas de web, métricas de Fresha, canales de adquisición.

### Documentación

Criterios financieros, criterios de marketing, criterios de sponsors, criterios de promociones, reglamentos internos, documentos legales, documentos contables, documentos de cooperativa, manuales operativos, documentos de marca.

### Memoria institucional

Consultas importantes, decisiones tomadas, eventos relevantes, reuniones, aprendizajes validados, fechas de revisión, resultados posteriores.

---

## 6. Qué no es Stylos OS

Stylos OS no es, al menos en su primera etapa:

- Una app propia
- Un reemplazo del contador
- Un sistema contable formal completo
- Un CRM que reemplace Fresha
- Un gestor de contraseñas
- Un sistema 100% automatizado
- Una IA que decide sola
- Un proyecto tecnológico por entusiasmo técnico

El sistema debe crecer cuando exista una necesidad real, no por complejidad innecesaria.

---

## 7. Estructura del proyecto

```
stylos-os/
  README.md
  SETUP.md
  .gitignore
  .env.example
  docs/
    00_vision/
    01_criterios/
    02_modelo-datos/
    03_procesos/
    04_prompts/
    05_templates/
    06_memoria/
      consultas/
      decisiones/
      aprendizajes/
      reuniones/
    07_documentos/
    tecnico/
      arquitectura.md
      instalacion.md
      changelog.md
      scripts/
      decisiones-tecnicas/
  scripts/
  data/
    raw/
    processed/
  backups/
```

---

## 8. Descripción de carpetas

| Carpeta | Propósito |
|---------|-----------|
| `docs/00_vision/` | Visión del sistema, objetivos, principios de diseño |
| `docs/01_criterios/` | Criterios de gestión: financieros, sponsors, promociones, marketing, operativos |
| `docs/02_modelo-datos/` | Documentación de fuentes de datos, hojas de Google Sheets, glosario |
| `docs/03_procesos/` | Procesos operativos: cierre diario, ingresos, egresos, liquidaciones |
| `docs/04_prompts/` | Prompts para análisis con IA: contexto, instrucciones, ejemplos |
| `docs/05_templates/` | Plantillas reutilizables: cierre diario, informes, evaluaciones |
| `docs/06_memoria/` | Memoria institucional: consultas, decisiones, aprendizajes, reuniones |
| `docs/07_documentos/` | Referencia a documentos legales, contables, de marca, reglamentos |
| `docs/tecnico/` | Documentación técnica: arquitectura, instalación, changelog, scripts |
| `scripts/` | Scripts de utilidad (futuro, cuando se justifiquen) |
| `data/raw/` | Datos exportados sin procesar |
| `data/processed/` | Datos procesados, limpios o transformados |
| `backups/` | Respaldo de datos críticos |

---

## 9. Regla obligatoria de documentación técnica

Todo script, automatización, cambio técnico o decisión de infraestructura debe quedar documentado para que otra persona con conocimiento pueda entenderlo, mantenerlo o corregirlo.

Esto aplica a:

- Scripts en `scripts/` o `docs/tecnico/scripts/`
- Cambios de arquitectura (documentar en `docs/tecnico/decisiones-tecnicas/`)
- Automatizaciones (cuando se implementen)
- Integraciones con APIs o servicios externos

La documentación técnica no es opcional. Si no está documentado, no existe.

---

## 10. Criterio para usar OpenCode

OpenCode (o cualquier agente de IA similar) puede usarse como herramienta de asistencia para:

- Analizar datos exportados y generar resúmenes
- Redactar o mejorar documentación
- Ayudar a mantener la memoria institucional
- Comparar escenarios y detectar riesgos
- Sugerir preguntas útiles para la gestión

**Reglas de uso:**

- OpenCode no toma decisiones por el negocio. Las decisiones las toma una persona.
- Todo análisis generado debe ser verificado antes de usarse para decidir.
- Los prompts utilizados deben guardarse en `docs/04_prompts/` para su reutilización y mejora continua.
- OpenCode debe recibir contexto real del negocio (datos, criterios, eventos). Sin contexto, sus respuestas son genéricas y menos útiles.

### Skills locales de OpenCode

El proyecto incluye skills locales que OpenCode carga automáticamente para proporcionar contexto especializado. Están en `.opencode/skills/`:

| Skill | Propósito |
|-------|-----------|
| `documentacion-tecnica` | Reglas de documentación técnica obligatoria |
| `arquitectura-incremental` | Principio de arquitectura gradual, evitar sobreingeniería |
| `sheets-base-datos` | Google Sheets como fuente de datos principal |
| `calidad-datos` | Validación y consistencia de datos |
| `memoria-institucional` | Formato y convenciones para memoria institucional |
| `seguridad-secretos` | Políticas de seguridad y manejo de secretos |

---

## 11. Criterio para usar IA

La IA dentro de Stylos OS debe actuar como:

- Analista de datos y documentos
- Auditor de supuestos
- Organizador de información
- Asistente de redacción
- Comparador de escenarios
- Generador de preguntas útiles
- Apoyo para interpretar información del negocio

**Restricciones:**

- La IA no decide. Las decisiones importantes son revisadas por una persona.
- La IA trabaja con contexto real del negocio: datos económicos, eventos, decisiones anteriores, criterios internos, documentos relevantes, restricciones financieras, objetivos comerciales y contexto argentino.
- Sin ese contexto, la IA puede dar respuestas genéricas. Con ese contexto, puede convertirse en una herramienta de criterio.
- Todo uso de IA debe quedar registrado (prompt, respuesta, verificación humana).

---

## 12. Flujo inicial recomendado

El orden sugerido para comenzar a usar Stylos OS es:

1. Leer la visión del sistema (`docs/00_vision/vision-stylos-os.md`)
2. Leer `SETUP.md` para configurar el entorno
3. Documentar las hojas de Google Sheets actuales en `docs/02_modelo-datos/`
4. Definir criterios básicos en `docs/01_criterios/`
5. Documentar procesos operativos en `docs/03_procesos/`
6. Comenzar a registrar decisiones y aprendizajes en `docs/06_memoria/`
7. Identificar documentos importantes en `docs/07_documentos/`
8. Crear plantillas útiles en `docs/05_templates/`
9. Usar IA con prompts guardados en `docs/04_prompts/`

---

## 13. Primer alcance mínimo

La primera versión útil de Stylos OS debe incluir:

- Repositorio ordenado con esta estructura
- Visión del sistema documentada
- Documentación de las hojas de Google Sheets actuales
- Hoja/archivo de eventos del negocio
- Registro de decisiones tomadas
- Registro de consultas a IA
- Registro de aprendizajes validados
- Criterios financieros básicos
- Criterios para sponsors
- Criterios para promociones
- Formato estructurado de cierre diario
- Prompt semanal de análisis guardado
- Memoria institucional en Markdown

No requiere todavía (son fases futuras potenciales): PostgreSQL, Metabase, n8n, OpenClaw, IA local, app propia, dashboards automáticos, automatizaciones de procesos.

---

## 14. Definición de éxito

Stylos OS será exitoso si logra que Stylo's Barber pueda:

- Entender mejor sus números
- Detectar problemas antes
- Evaluar inversiones con punto de equilibrio
- Medir promociones y sponsors
- Ordenar documentos importantes
- Registrar decisiones y aprendizajes
- Reducir dependencia de la memoria personal
- Facilitar una eventual transición cooperativa
- Usar IA con contexto real y no con información suelta

El éxito del proyecto no se mide por la cantidad de herramientas usadas, sino por la calidad de las decisiones que permite tomar.

---

## 15. Definición corta

Stylos OS es la memoria de gestión de Stylo's Barber: un sistema gradual para ordenar datos, documentos, decisiones y aprendizajes, con el objetivo de tomar mejores decisiones económicas, comerciales y operativas.

---

Para la configuración inicial, ver [SETUP.md](SETUP.md).
Para el detalle completo de la visión, ver [docs/00_vision/vision-stylos-os.md](docs/00_vision/vision-stylos-os.md).
