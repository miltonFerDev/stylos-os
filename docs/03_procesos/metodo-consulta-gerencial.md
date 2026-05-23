# Método de consulta gerencial

## Objetivo

Documentar un método para responder consultas libres de gestión. La consulta parte del usuario, no del sistema. Este método no predefine ni limita las preguntas posibles. No existe un menú cerrado de consultas objetivo.

El objetivo es proporcionar un marco para clasificar, analizar y responder cualquier consulta que surja de la gestión del negocio, con honestidad sobre qué datos están disponibles y qué nivel de confianza tiene la respuesta.

---

## 1. Recibir una consulta libre

### Principio

El usuario formula la pregunta en lenguaje natural, con sus propias palabras. No se le presenta una lista de opciones predefinidas. La consulta llega por cualquier canal: conversación directa, mensaje, WhatsApp, email.

### Pasos

1. El usuario plantea su consulta sin que se le haya sugerido qué preguntar.
2. Se registra la consulta textualmente, con las palabras exactas del usuario.
3. Se identifica el contexto: por qué surge la consulta ahora, qué situación la motiva.
4. Se procede a clasificar por área (sección 2).

### Qué NO se hace

- No se muestra un menú de preguntas predefinidas.
- No se condiciona al usuario a formular la consulta de una manera específica.
- No se asume que la primera interpretación es la única posible.

---

## 2. Clasificar por área

### Áreas disponibles

La clasificación es orientativa. Una consulta puede pertenecer a un área principal y a una o más áreas secundarias.

| Área | Descripción |
|------|-------------|
| **Finanzas** | Ingresos, egresos, resultados, margen, flujo de caja, rentabilidad |
| **Operación** | Día a día del local, turnos, servicios, productos, tiempos, occupancy |
| **Marketing** | Promociones, campaigns, redes sociales, clientela nueva vs recurrente |
| **Equipo** | Comisiones, presencia, licencias, rotación, distribución de servicios |
| **Caja** | Arqueo, medios de pago, efectivo disponible, conciliaciones |
| **Inversión** | Compras de equipos, mejoras del local, activos, gasto de capital |
| **Precios** | Valor de servicios, ajustes de precio, paquetes, promociones de precio |
| **Sponsor / Alianza** | Convenios, sponsorship, partnerships, beneficios no operativos |
| **Signos vitales** | Indicadores clave de salud del negocio, métricas de tendencia |
| **Otra** | Cualquier área que no corresponda a las anteriores |

### Cómo clasificar

- **Área principal**: la que mejor describe el objetivo central de la consulta.
- **Áreas secundarias**: las que también están relacionadas, aunque sea tangencialmente.

### Ejemplo (marcado explícitamente como ejemplo, no como menú)

> **Consulta del usuario**: "Quiero saber si conviene renovar el aire acondicionado con el sponsor de siempre o buscar otro."
> - Área principal: **Inversión**
> - Áreas secundarias: **Sponsor / Alianza**, **Finanzas**, **Signos vitales**
>
> Este es un ejemplo ilustrativo. No es una opción de un menú.

---

## 3. Identificar fuentes de datos

Una vez clasificada la consulta, se determina qué fuentes de datos pueden aportar información para responderla.

### Fuentes disponibles actualmente

| Fuente | Tipo | Qué contiene |
|--------|------|---------------|
| Google Sheets — Caja_diaria | Dato crudo | Ingresos diarios por medio de pago |
| Google Sheets — Egresos | Dato crudo | Gastos detallados por categoría y persona |
| Google Sheets — Comisiones | Dato crudo | Comisiones diarias por barbero |
| Google Sheets — Cuota parte | Análisis | Distribución de ingresos por cuota parte |
| Google Sheets — Presupuesto | Análisis | Presupuesto y ejecución |
| Google Sheets — Dashboard | Análisis | Indicadores resumen |
| Fresha | CRM / Plataforma | Turnos, clientes, servicios |
| Cuaderno físico / Hoja diaria | Registro operativo | Detalle por jornada |

### Mapeo por área

| Área | Fuentes probables |
|------|-----------------|
| Finanzas | Caja_diaria, Egresos, Cuota parte, Presupuesto |
| Operación | Fresha, Hoja diaria, Comisiones |
| Marketing | Fresha (clientes nuevos vs recurrentes), caja en períodos promocionales |
| Equipo | Comisiones, Personas, Hoja diaria |
| Caja | Caja_diaria, Egresos |
| Inversión | Egresos (categoría), Presupuesto, Cuota parte |
| Precios | Egresos (categoría), caja en períodos con/sin promoción |
| Sponsor / Alianza | Egresos, Eventos, Decisiones |
| Signos vitales | Dashboard, Caja_diaria, Egresos, Cuota parte |

Para el detalle de cada fuente, ver `../02_modelo-datos/estructura-sheets.md` y `../02_modelo-datos/diccionario-datos.md`.

### Fuentes pendientes de relevar

Algunas hojas aún no fueron verificadas contra las planillas reales:

- Personas
- Categorías
- Subcategorías
- Medios de pago
- Eventos
- Decisiones
- Consultas IA
- Aprendizajes

Si la consulta requiere datos de una hoja pendiente, se documenta como dato faltante (sección 5).

---

## 4. Cruces posibles

No toda consulta puede responderse con un solo dato. Muchas requieren cruzar información de distintas fuentes. Esta sección describe qué cruces son posibles hoy, cuáles están parcialmente disponibles y cuáles se desean a futuro.

### Cruces posibles hoy (datos verificados y documentados)

| Cruce | Fuentes | Qué responde |
|-------|---------|---------------|
| Ingresos diarios por medio de pago | Caja_diaria × propia | Total por Efectivo, MPD, MPM, Tarjeta por día |
| Egresos por categoría | Egresos × Categorías | Gastos agrupados por tipo |
| Comisiones por barbero por día | Comisiones × Personas | Quién trabajó, cuántos servicios, cuánto cobró |
| Resultado operativo diario | Caja_diaria × Egresos | Ingresos menos egresos del día |
| Margen operativo por período | Caja_diaria × Egresos × Período | Resultado operativo como % de ingresos |

### Cruces posibles parcialmente (datos disponibles pero con limitaciones)

| Cruce | Limitación | Referencia |
|-------|-----------|------------|
| Egresos por persona | PersonaID frecuentemente vacío en Egresos | V-EG-10 en `../02_modelo-datos/plan-validaciones-sheets.md` |
| Comisiones × Egresos por barbero | No hay clave común documentada para cruzar ambas hojas | Validación cruzada V-CR-01 pendiente |
| Signos vitales por semana/mes | No hay Dashboard verificado contra planillas reales | Hoja Dashboard pendiente de relevar |
| Cuota parte real | Hoja Cuota parte pendiente de relevar completo | Depende de confirmación de fórmula |

### Cruces deseados a futuro (requieren datos que aún no se relevan)

| Cruce | Datos faltantes |
|-------|----------------|
| Ocupancy rate por barbero | Necesita relación turns/disponibilidad horaria en Fresha |
| Costo de adquisición de cliente | Necesita datos de marketing digital (Meta/Instagram) |
| ROI por promoción | Necesita clasificar egresos promocionales vs operativos |
| Evolución de clientela nueva vs recurrente | Necesita datos de Fresha con segmento de clientela |
| Proyección de caja a 30/60/90 días | Necesita datos consistentes de Egresos por categoría + Presupuesto |

Las validaciones cruzadas propuestas están documentadas en `../02_modelo-datos/plan-validaciones-sheets.md` (V-CR-01 a V-CR-05).

---

## 5. Datos faltantes

### Cómo detectar que faltan datos

Una consulta no puede responderse cuando:

- La fuente necesaria no existe o no fue relevada.
- La fuente existe pero tiene campos vacíos o incompletos de forma sistemática.
- Se requiere un dato que depende de otra fuente no disponible.
- El cruce entre fuentes no está documentado ni validado.

### Pasos ante datos faltantes

1. Identificar qué dato específico falta.
2. Clasificar la limitación: dato inexistente, incompleto, o no cruzable.
3. Estimar el esfuerzo de completar el dato (relevar una hoja, confirmar una fórmula, etc.).
4. Decidir: ¿se responde con los datos disponibles acknowledging la limitación (sección 6), o se postponela respuesta hasta tener el dato?

### Hojas con datos pendientes de relevar

Estas hojas tienen campos marcados como `TODO` en `../02_modelo-datos/diccionario-datos.md`:

- Cuota parte
- Presupuesto
- Dashboard
- Personas
- Categorías
- Subcategorías
- Medios de pago
- Eventos
- Decisiones
- Consultas IA
- Aprendizajes

Si la consulta depende de alguna de estas hojas, se trata como dato faltante hasta que se complete el relevamiento.

---

## 6. Nivel de confianza

Toda respuesta a una consulta gerencial debe incluir su nivel de confianza. Esto permite al usuario saber qué tan respaldada está la respuesta y tomar decisiones con esa información.

| Nivel | Significado | Condición |
|-------|-------------|-----------|
| **Confirmado** | Respaldado por datos documentados y verificados | Los datos existen, están completos y fueron validados contra la fuente |
| **Probable** | Respaldado por datos disponibles, pero con alguna limitación | Los datos existen pero tienen gaps de completitud, no fueron validados recientes, o dependen de supuestos menores |
| **Estimado** | Respaldado por supuestos o datos parciales | Se requiere hacer inferencias, promedios, o extrapolaciones para construir la respuesta |
| **No disponible** | No hay datos suficientes para responder con seriedad | La fuente no existe, está vacía, o la consulta requiere información que no se puede inferir |

### Cómo comunicar cada nivel

- **Confirmado**: "Los datos de Caja_diaria muestran que..."
- **Probable**: "Según los datos disponibles de Egresos, es probable que..., aunque hay que aclarar que..."
- **Estimado**: "No tenemos el dato exacto, pero basándonos en [supuesto], podemos estimar que..."
- **No disponible**: "No tenemos datos para responder esta consulta. Para poder responderla sería necesario..."

### Principio

No inflar el nivel de confianza. Si hay duda entre probable y confirmado, optar por el menor. La honestidad sobre la calidad del dato es más útil que una falsa precisión.

---

## 7. Registrar la consulta

No toda consulta se registra. Una consulta se registra en `../06_memoria/consultas/` solo si cumple al menos una de las siguientes condiciones:

- **Afecta una decisión relevante**: la respuesta puede cambiar una acción o dirección del negocio.
- **Puede repetirse en el futuro**: es una pregunta que probablemente volverá a hacerse.
- **Genera aprendizaje**: la respuesta reveló algo que no se sabía o confirmó una intuición.
- **Evidencia una duda recurrente**: aparece en múltiples consultas relacionadas.
- **Impacta en finanzas, operación, marketing, equipo o estrategia**: tiene peso en alguna de estas áreas clave.

### Criterio de descarte

Si la consulta es:

- Un dato puntual que no tiene consecuencias broader.
- Una pregunta hipotética sin impacto en decisiones.
- Una consulta única que no se repetirá.

...no se registra. Se responde directamente sin entrar al registro de memoria.

### Formato de registro

Ver `../06_memoria/consultas/registro-consulta.md` para la plantilla completa. En resumen, cada registro debe incluir:

- Fecha de la consulta
- Texto original de la consulta
- Contexto (por qué surge)
- Área(s) clasificada(s)
- Respuesta y nivel de confianza
- Fuente de la respuesta
- Relevancia futura

---

## 8. Convertir en decisión o aprendizaje

Algunas consultas, por su impacto o recurrencia, merecen trascender el registro de consulta y convertirse en una decisión o un aprendizaje.

### Convertir en decisión

Se convierte en decisión cuando:

- La respuesta implica elegir entre dos o más cursos de acción.
- Hay criterios definidos para evaluar las opciones.
- La decisión tomada debe registrarse para futura auditoría.

**Formato**: `../06_memoria/decisiones/registro-decision.md`

### Convertir en aprendizaje

Se convierte en aprendizaje cuando:

- La consulta reveló algo que contradice una suposición anterior.
- El resultado de actuar sobre la respuesta fue diferente al esperado.
- Se validó o refutó un criterio existente con datos.

**Formato**: `../06_memoria/aprendizajes/registro-aprendizaje.md`

### Criterio general

Si la consulta solo genera una respuesta útil pero no cambia nada en el negocio, se registra como consulta. Si de la consulta resulta un cambio de criterio, una acción tomada, o una lección validada, corresponde pasarla a decisión o aprendizaje.

---

## Qué NO hace este método

- **No crea listas cerradas de preguntas.** Los ejemplos son ilustrativos, no opciones de un menú.
- **No condiciona al usuario.** La consulta parte del usuario, siempre.
- **No automatiza nada.** No se crean scripts, integraciones, ni flujos automatizados.
- **No modifica Google Sheets.** El modelo de datos no se toca desde aquí.
- **No propone PostgreSQL ni otra base de datos.** La fuente de datos son las planillas existentes.
- **No prescribe respuestas.** Solo ofrece un marco para clasificar, analizar y responder con transparencia sobre la calidad del dato.

---

## Referencias

- Estructura de Sheets: `../02_modelo-datos/estructura-sheets.md`
- Diccionario de datos: `../02_modelo-datos/diccionario-datos.md`
- Plan de validaciones: `../02_modelo-datos/plan-validaciones-sheets.md`
- Cierre diario: `../03_procesos/cierre-diario.md`
- Memoria institucional — Consultas: `../06_memoria/consultas/`
- Memoria institucional — Decisiones: `../06_memoria/decisiones/`
- Memoria institucional — Aprendizajes: `../06_memoria/aprendizajes/`
