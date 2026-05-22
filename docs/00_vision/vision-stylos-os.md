# Visión de Stylos OS

## Propósito

Definir qué es Stylos OS, qué problema resuelve, cuál es su objetivo y cuáles son sus principios de diseño. Este documento es la referencia central para entender la dirección del proyecto.

---

## 1. Qué es Stylos OS

Stylos OS es un sistema interno de gestión e inteligencia para Stylo's Barber.

Su objetivo es centralizar y ordenar la información económica, operativa, comercial y documental del negocio para mejorar la toma de decisiones.

No nace como una app, ni como un dashboard, ni como una automatización aislada. Nace como una **memoria institucional y analítica** del negocio.

Stylos OS debe ayudar a responder preguntas concretas de gestión:

- ¿Cuánto ganó realmente el negocio?
- ¿Qué cambió respecto al período anterior?
- ¿Qué gastos se desordenaron?
- ¿Podemos asumir un costo nuevo?
- ¿Conviene hacer una promoción, sponsor o alianza?
- ¿Qué datos explican una baja o suba de clientes?
- ¿Qué aprendimos de decisiones anteriores?
- ¿Qué documento o criterio respalda una decisión?

El sistema debe servir tanto para la estructura actual de Stylo's Barber como para una posible futura estructura cooperativa.

## 2. Problema que busca resolver

Actualmente, la información del negocio existe, pero está distribuida en distintos lugares:

- Google Sheets
- Fresha
- WhatsApp
- Cuaderno físico de cierre diario
- Google Drive
- Meta/Instagram
- Web y analíticas
- Documentos sueltos
- Memoria personal de quienes gestionan

Esto genera varios problemas:

- Dificultad para ver el estado real del negocio
- Dependencia excesiva de la memoria de una o pocas personas
- Decisiones tomadas con información incompleta
- Dificultad para revisar si una acción funcionó o no
- Carga administrativa repetida
- Riesgo de errores en datos cargados manualmente
- Falta de trazabilidad entre decisión, ejecución y resultado
- Poca conexión entre marketing, operación y finanzas

Stylos OS busca ordenar ese ecosistema sin romper los procesos que ya funcionan.

## 3. Objetivo principal

El objetivo principal de Stylos OS es permitir que Stylo's Barber pase de decidir en base a sensaciones dispersas a decidir con:

- Datos confiables
- Contexto operativo
- Criterios definidos
- Documentos accesibles
- Historial de decisiones
- Aprendizajes acumulados
- Análisis asistido por IA cuando sea útil

La meta no es automatizar todo. La meta es **mejorar la calidad de decisión**.

## 4. Principio central

Primero utilidad de gestión. Después tecnología.

Cada avance de Stylos OS debe justificar su existencia porque mejora alguna de estas cosas:

- Reduce errores
- Ahorra tiempo administrativo
- Mejora una decisión
- Aclara un dato
- Ordena un proceso
- Deja trazabilidad
- Permite aprender de lo hecho
- Facilita una futura cooperativa

Si una herramienta, script, dashboard o automatización no mejora alguno de esos puntos, no debe priorizarse.

## 5. Qué incluye Stylos OS

Stylos OS incluye, de forma progresiva:

### Datos económicos

- Ingresos diarios
- Egresos
- Comisiones
- Sueldos
- Retiros
- Presupuesto
- Fondos
- Resultado operativo
- Margen
- Caja proyectada

### Datos operativos

- Servicios
- Barberos
- Medios de pago
- Cierres diarios
- Eventos del negocio
- Datos de Fresha cuando estén disponibles

### Datos comerciales y de marketing

- Campañas
- Promociones
- Sponsors
- Alianzas
- Métricas de Instagram
- Métricas de web
- Métricas de Fresha
- Canales de adquisición

### Documentación

- Criterios financieros
- Criterios de marketing
- Criterios de sponsors
- Criterios de promociones
- Reglamentos internos
- Documentos legales
- Documentos contables
- Documentos de cooperativa
- Manuales operativos
- Documentos de marca

### Memoria institucional

- Consultas importantes
- Decisiones tomadas
- Eventos relevantes
- Reuniones
- Aprendizajes validados
- Fechas de revisión
- Resultados posteriores

## 6. Qué no es Stylos OS

Stylos OS no es, al menos en su primera etapa:

- Una app propia
- Un reemplazo del contador
- Un sistema contable formal completo
- Un CRM que reemplace Fresha
- Un gestor de contraseñas
- Un sistema 100% automatizado
- Una IA que decide sola
- Una herramienta para complicar la carga diaria
- Un proyecto tecnológico por entusiasmo técnico

Stylos OS debe apoyarse en herramientas simples mientras sean suficientes.

## 7. Usuario inicial

El usuario inicial de Stylos OS es Milton, como responsable de gestión, análisis y toma de decisiones.

En el futuro, el sistema podría servir también a:

- Administración
- Contador
- Socios
- Recepción
- Barberos
- Órganos de una eventual cooperativa

Pero el diseño inicial debe evitar complejidad multiusuario hasta que exista una necesidad real.

## 8. Relación con la futura cooperativa

Stylos OS debe estar pensado para funcionar tanto en la barbería actual como en una futura cooperativa.

Esto implica que el sistema debe favorecer:

- Transparencia
- Trazabilidad
- Criterios claros
- Documentación ordenada
- Reglas de decisión
- Registro de eventos y acuerdos
- Separación entre datos, análisis y decisiones
- Capacidad de explicar por qué se tomó una decisión

En una cooperativa, no alcanza con que una persona "sepa" qué pasó. El conocimiento debe quedar institucionalizado. Por eso, Stylos OS debe transformar memoria personal en memoria organizacional.

## 9. Criterio de avance

Stylos OS debe avanzar por fases. No se debe construir infraestructura compleja hasta que haya una versión simple funcionando.

El orden correcto es:

1. Ordenar datos y documentos existentes
2. Mejorar el registro diario
3. Crear memoria institucional
4. Definir criterios de gestión
5. Validar calidad de datos
6. Crear reportes simples
7. Usar IA de forma manual con contexto ordenado
8. Recién después automatizar procesos
9. Recién después evaluar PostgreSQL, Metabase, n8n, IA local u otras herramientas
10. Recién al final considerar una app propia

La pregunta antes de cada avance debe ser: **¿Esto mejora la gestión real del negocio o solo agrega complejidad?**

## 10. Rol de la IA

La IA dentro de Stylos OS no debe actuar como una autoridad que decide por el negocio.

Debe actuar como:

- Analista
- Auditor de supuestos
- Organizador de información
- Asistente de redacción
- Comparador de escenarios
- Ayudante para detectar riesgos
- Generador de preguntas útiles
- Apoyo para interpretar datos y documentos

La IA debe trabajar con contexto real del negocio:

- Datos económicos
- Eventos
- Decisiones anteriores
- Criterios internos
- Documentos relevantes
- Restricciones financieras
- Objetivos comerciales
- Contexto argentino

Sin esos elementos, la IA puede dar respuestas genéricas. Con esos elementos, puede convertirse en una herramienta de criterio.

## 11. Ejemplo de uso esperado

Una consulta esperada sería:

> Estoy pensando en activar un sponsor en un club por $250.000 mensuales. ¿Qué te parece?

Stylos OS debería ayudar a responder:

- Qué costo representa sobre el resultado mensual
- Cuántos clientes nuevos necesita para cubrirse
- Si la caja permite asumirlo
- Si afecta el margen mínimo
- Si ayuda a ocupar horarios flojos
- Qué debería pedirse a cambio
- Cómo medirlo
- Cuánto tiempo probarlo
- Cuándo renovarlo o cortarlo
- Qué antecedentes similares existen

La respuesta ideal no es "sí" o "no", sino una **recomendación condicionada por datos, reglas y objetivos**.

## 12. Principios de diseño

### Simplicidad operativa

El sistema no debe hacer más difícil el trabajo diario. Si una mejora complica demasiado a recepción, administración o gestión, debe revisarse.

### Datos antes que automatización

Primero se ordenan los datos. Después se automatiza.

### Registro antes que memoria informal

Toda decisión importante debe quedar registrada con contexto, hipótesis, fecha de revisión y resultado posterior.

### Criterio antes que herramienta

La herramienta no reemplaza el criterio. Lo estructura.

### Documentación obligatoria

Todo script, automatización o cambio técnico debe quedar documentado para que otra persona con conocimiento pueda entenderlo, mantenerlo o corregirlo.

### Validación humana

La IA puede sugerir, resumir y analizar. Las decisiones relevantes deben ser revisadas por una persona.

### Evolución gradual

El sistema debe crecer cuando aparece un dolor real, no por entusiasmo técnico.

## 13. Primer alcance mínimo

La primera versión útil de Stylos OS debe incluir:

- Carpeta o repositorio ordenado
- Documentación de visión
- Documentación de las hojas actuales
- Hoja de eventos
- Hoja de decisiones
- Hoja de consultas IA
- Hoja de aprendizajes
- Criterios financieros básicos
- Criterios para sponsors
- Criterios para promociones
- Formato estructurado de cierre diario
- Dashboard mínimo de gestión
- Prompt semanal de análisis
- Memoria institucional en Markdown

No requiere todavía:

- PostgreSQL
- Metabase
- n8n
- OpenClaw
- IA local
- App propia

## 14. Resultado esperado

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

## 15. Definición corta

Stylos OS es la memoria de gestión de Stylo's Barber: un sistema gradual para ordenar datos, documentos, decisiones y aprendizajes, con el objetivo de tomar mejores decisiones económicas, comerciales y operativas.
