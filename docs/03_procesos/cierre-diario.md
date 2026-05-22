# Cierre diario — Proceso

## Objetivo

Documentar el proceso de cierre diario de Stylo's Barber: cómo se hace hoy, cuáles son sus límites, cómo se propone mejorarlo, y qué reglas gobiernan la transición al nuevo flujo.

Este documento no implementa cambios. Solo documenta el estado actual y el diseño del flujo propuesto.

---

## 1. Flujo actual

### Responsable

Recepción.

### Pasos

**Durante el día:**

1. Recepción registra servicio a servicio en un cuaderno anillado A5.
2. Cada registro incluye: nombre del cliente, inicial del barbero, inicial del servicio, medio de pago.
3. Egresos, pagos de comisión y retiros se registran en una fila completa del cuaderno, diferenciados de los servicios.

**Al cierre del día:**

4. Recepción revisa el cuaderno y arma un resumen por WhatsApp.
5. El mensaje se envía a la persona encargada de administración, pagos, caja grande y carga financiera.
6. El mensaje incluye un resumen de ingresos, comisiones, egresos y retiros del día.

**Post-cierre:**

7. Administración recibe el mensaje de WhatsApp.
8. Complementa la información con datos de Fresha (turnos, clientes, servicios), billeteras virtuales (MPD, MPM), bancos y posnet.
9. Administración realiza la carga periódica de datos financieros en Sheets (Caja_diaria, Egresos, Comisiones).

### Fuentes de datos usadas

| Fuente | Uso en el proceso |
|--------|-------------------|
| Cuaderno A5 | Registro primario de servicios, egresos, comisiones y retiros |
| Fresha | Doble registro / fuente complementaria de turnos y servicios |
| WhatsApp | Canal de comunicación del resumen de cierre |
| Mercado Pago (MPD, MPM) | Verificación de movimientos de billeteras |
| Bancos y posnet | Verificación de movimientos con tarjetas |
| Google Sheets | Carga y almacenamiento de datos financieros |

---

## 2. Problemas y límites del flujo actual

### Estructura del registro

- El cuaderno A5 es de formato libre: cada persona puede usar abreviaturas distintas.
- No hay una lista cerrada de tipos de movimiento (servicio, egreso, comisión, retiro, etc.).
- No hay una lista cerrada de medios de pago.
- La mezcla de servicios, egresos, comisiones y retiros en un mismo formato puede generar ambigüedades.

### Montos y legibilidad

- Los montos pueden escribirse de forma abreviada o con interpretacion personal (ej: "33" puede significar $33.000 o $33).
- Los nombres de barberos pueden variar en formato entre un mensaje y otro.
- No hay un formato estándar para el mensaje de WhatsApp; cada día puede verse diferente.

### Dependencia humana

- La calidad del cierre depende de la persona que opera recepción.
- No hay forma de validar automáticamente que los números cierren.
- El paso a Sheets depende de que alguien traduzca el mensaje a datos.

### Trazabilidad

- El cuaderno no tiene numeración ni fechar autor.
- Si se pierde el mensaje de WhatsApp, no hay un respaldo estructurado.
- No hay forma fácil de auditar qué pasó en un día específico sin revisar manualmente el cuaderno y el mensaje.

### Relación con Sheets

- El paso de WhatsApp a Sheets no está estructurado: requiere traducción manual.
- No hay validación de que los números del mensaje coincidan con lo cargado en Sheets.
- Fresha existe como fuente complementaria pero no reemplaza el registro manual.

---

## 3. Flujo propuesto mejorado

### Principio

Mantener el registro manual físico porque es rápido y útil para recepción. Mejorar la estructura sin perder velocidad operativa.

### Objetivo del nuevo registro físico

- Servir como control de caja y respaldo operativo.
- Permitir el armado del mensaje de cierre WhatsApp sin tener que re-intercalar datos.
- No reemplazar Fresha como CRM ni duplicar todos sus datos.
- Ser legible por personas y, en el futuro, parseable por scripts (sin automatización todavía).

### Nuevo formato de registro: hoja diaria

**Formato:** A4 apaisado (horizontal), imprimible en papel o usable en pantalla.
**Uso:** Recibir el registro manual de la jornada y calcular totales al pie.
**Responsable del registro:** Recepción.

### Estructura de la hoja diaria

**Columnas:**

| # | Columna | Descripción |
|---|---------|-------------|
| 1 | N° | Número correlativo de fila |
| 2 | Hora | Hora del registro (opcional, puede omitirse en días de bajo movimiento) |
| 3 | Tipo | Categoría del movimiento. Valores válidos: Servicio, Producto, Egreso, Comisión, Retiro, Ajuste, Seña, Otro |
| 4 | Cliente / Detalle | Nombre del cliente para servicios. Descripción breve para egresos u otros tipos. |
| 5 | Barbero | Inicial o nombre del barbero. Usar siempre el mismo formato. |
| 6 | Servicio | Inicial o nombre del servicio realizado. |
| 7 | Medio de pago | Efectivo, MPD, MPM, Tarjeta, Transferencia, Otro |
| 8 | Ingreso | Monto de dinero que entra. Solo para Tipo = Servicio, Producto, Seña, Ajuste. |
| 9 | Salida | Monto de dinero que sale. Solo para Tipo = Egreso, Comisión, Retiro. |
| 10 | Observación | Espacio para aclarar situaciones especiales (ej: "seña confirmación", "licencia médica", "ajuste por diferencia"). |

**Totales al pie de hoja:**

| Concepto | Monto |
|---------|-------|
| Total ingresos efectivo | (suma de Ingreso donde Medio de pago = Efectivo) |
| Total MPD | (suma de Ingreso donde Medio de pago = MPD) |
| Total MPM | (suma de Ingreso donde Medio de pago = MPM) |
| Total tarjetas | (suma de Ingreso donde Medio de pago = Tarjeta) |
| Total transferencias | (suma de Ingreso donde Medio de pago = Transferencia) |
| **Total ingresos** | (suma de todos los Ingresos) |
| Total salidas | (suma de todos los Salidas) |
| Comisiones pagadas | (suma de Salidas donde Tipo = Comisión) |
| Egresos extraordinarios | (suma de Salidas donde Tipo = Egreso) |
| Retiros | (suma de Salidas donde Tipo = Retiro) |
| **Caja final esperada** | (Total ingresos - Total salidas) |
| Caja final contada | (monto que efectivamente hay en caja) |
| **Diferencia** | (Caja final contada - Caja final esperada) |
| Observaciones | (espacio para notas sobre diferencias, ajustes, situaciones especiales) |

### Valores válidos para Tipo

- **Servicio:** Pago por corte, barba, tratamiento u otro servicio de barbería.
- **Producto:** Venta de producto (pomada, aceite, shampoo, etc.).
- **Egreso:** Gasto extraordinario del local (insumos, mantenimiento, servicios, etc.).
- **Comisión:** Pago de comisión a barbero.
- **Retiro:** Retiro de dinero de caja por parte de socio o responsable.
- **Ajuste:** Corrección de un monto anterior (diferencia, devolución, corrección).
- **Seña:** Anticipo o seña por servicio futuro confirmado.
- **Otro:** Cualquier movimiento que no corresponda a las categorías anteriores.

### Valores válidos para Medio de pago

- **Efectivo:** Billetes y monedas.
- **MPD:** Mercado Pago débito / cuotas.
- **MPM:** Mercado Pago mercado / monedero / link de pago.
- **Tarjeta:** Tarjeta de crédito o débito (no Mercado Pago).
- **Transferencia:** Transferencia bancaria u otro medio no listado.
- **Otro:** Medio no contemplado en las categorías anteriores.

### Notas sobre Transferencia

El formato de registro físico contempla Transferencia como medio de pago operativo. Sin embargo, el modelo actual de datos en Sheets (hoja Caja_diaria) no incluye una columna para Transferencia; solo contempla Efectivo, MPD, MPM y Tarjetas.

**No se debe modificar el modelo de datos de Sheets en este sprint.** Si se registra una transferencia en el formato físico, se debe indicar como Observación o agrupar bajo el medio más cercano disponible al momento de la carga en Sheets. Esta discrepancia se documenta como observación para evaluación futura.

### Proceso de uso de la hoja diaria

1. Recepción inicia la jornada con una hoja diaria en blanco (impresa o en pantalla).
2. Cada vez que ocurre un movimiento (servicio, egreso, etc.), se registra una fila.
3. Al cierre de la jornada, se calculan los totales al pie.
4. Se verifica que la caja contada coincida con la caja esperada. Si hay diferencia, se anota en Observaciones.
5. Con los totales, se arma el mensaje de WhatsApp usando el formato estandarizado.
6. El cuaderno físico y/o la hoja impresa se archiva como respaldo.

---

## 4. Reglas de transición

Al adoptar el nuevo formato de registro físico, aplican las siguientes reglas:

**Registro diario:**

- Usar el nuevo formato para todo registro nuevo. No retroalimentar días anteriores.
- Si un día no se usó el formato, registrarlo con el método anterior y agregar una observación.
- Mantener Fresha como doble registro y fuente complementaria, no reemplazarlo.

**Carga en Sheets:**

- La carga sigue siendo responsabilidad de administración, como hasta ahora.
- El nuevo formato facilita la traducción de mensaje a datos, pero no la automatiza.
- No implementar scripts de carga automática en este sprint.

**WhatsApp:**

- Usar el formato estandarizado de mensaje de cierre (ver template en `../05_templates/cierre-diario-whatsapp.md`).
- Comenzar a usar el nuevo formato a partir de una fecha acordada.
- Los cierres anteriores no se reprograman; quedan en el formato en que se enviaron.

**Discrepancias de medio de pago:**

- Si el registro físico incluye Transferencia, aclararlo en el mensaje de WhatsApp y en la observación de la hoja.
- No agrupar Transferencia bajo otro medio para forzar compatibilidad con Sheets.
- Documentar la Transferencia como observación para evaluación futura del modelo.

**Diferencias de caja:**

- Si la caja contada no coincide con la caja esperada, registrar la diferencia en Observaciones con contexto.
- No ajustar montos sin registro. Toda diferencia debe tener una explicación escrita.

---

## 5. Qué no se implementa todavía

Las siguientes acciones están fuera del alcance de este sprint:

- **Scripts de carga automática** — La traducción de mensaje WhatsApp a Sheets se sigue haciendo manualmente.
- **Automatización de WhatsApp** — El mensaje se arma y se envía manualmente.
- **Modificación del modelo de datos en Sheets** — La incorporación de Transferencia como columna de Caja_diaria no está en el alcance de este sprint.
- **Validaciones automáticas** — No se implementan scripts que detecten errores o inconsistencias.
- **Reemplazo de Fresha** — Fresha sigue siendo el sistema de turnos y CRM.
- **Plantilla digital interactiva** — El formato es para papel o PDF; no se diseña una plantilla con validaciones dinámicas.
- **Integración con n8n, PostgreSQL u otras herramientas** — Estas quedan fuera hasta que el flujo manual esté validado.

---

## Referencias

- Template de registro diario físico: `../05_templates/registro-diario-fisico.md`
- Template de cierre WhatsApp: `../05_templates/cierre-diario-whatsapp.md`
- Proceso de carga en Sheets: PENDIENTE (documentar cuando se confirme el flujo)
- Modelo de datos: `../02_modelo-datos/estructura-sheets.md`