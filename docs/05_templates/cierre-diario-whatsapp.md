# Cierre diario WhatsApp — Template

## Propósito

Formato estándar para el mensaje de cierre diario que envía recepción a administración por WhatsApp.

**Responsable:** Recepción.
**Destinatario:** Administración.
**Frecuencia:** Al final de cada jornada.

---

## Objetivo del formato

- Que el mensaje sea legible por una persona.
- Que los datos sean consistentes día a día.
- Que el formato esté preparado para futuro parseo automático (sin automatización todavía).
- Que no haya ambigüedades en montos, nombres o medios de pago.

---

## Formato del mensaje

```
CIERRE
fecha: YYYY-MM-DD

COMISIONES
Nombre | efectivo: monto | mp: monto

EGRESOS
monto | descripción

RETIROS
concepto | monto

TARJETAS
monto

OBSERVACIONES
texto o -
```

---

## Secciones obligatorias

Todas las secciones deben aparecer siempre, aunque estén vacías. Si una sección no tiene datos, escribir un guión (`-`) en lugar de omitirla.

### 1. Encabezado

```
CIERRE
fecha: 2026-05-22
```

- `CIERRE` siempre en mayúsculas.
- Fecha en formato `YYYY-MM-DD` (año-mes-día, con guiones).

### 2. Comisiones

```
COMISIONES
M | efectivo: 15000 | mp: 8500
F | efectivo: 12000 | mp: 0
J | efectivo: 0 | mp: 43000
```

- Un línea por barbero.
- Usar la inicial del nombre (M, F, J, etc.) o el nombre completo si se prefiere consistencia.
- Siempre incluir `efectivo:` y `mp:` aunque el valor sea 0.
- Si no hay comisiones en el día, escribir:

```
COMISIONES
-
```

### 3. Egresos

```
EGRESOS
8500 | Insumos limpieza
12000 | Gasoil
```

- Formato: `monto | descripción`.
- Un línea por egreso.
- La descripción debe ser clara y breve.
- Si no hay egresos en el día, escribir:

```
EGRESOS
-
```

### 4. Retiros

```
RETIROS
Retiro semana | 15000
```

- Formato: `concepto | monto`.
- Un línea por retiro.
- Si no hay retiros en el día, escribir:

```
RETIROS
-
```

### 5. Tarjetas

```
TARJETAS
35000
```

- Escribir solo el monto total de tarjetas del día (crédito, débito, no Mercado Pago).
- No desglosar por entidad ni por tipo de tarjeta.
- Si no hay movimientos con tarjeta en el día, escribir:

```
TARJETAS
0
```

### 6. Observaciones

```
OBSERVACIONES
Seña confirmada para 23/05 con Pedro Gómez. Cliente nuevo derivó por Instagram.
```

- Espacio para anotar situaciones especiales: señas, licencias, ajustes, diferencias de caja, cliente nuevo, etc.
- Si no hay observaciones, escribir:

```
OBSERVACIONES
-
```

---

## Reglas de formato

### Montos

- **Siempre escribir el monto completo.** No usar abreviaturas.
- `15000` significa quince mil pesos, no quince.
- `35000` significa treinta y cinco mil pesos, no treinta y cinco.
- Si el monto es cero, escribir `0`. No dejar vacío.

### Nombres de barberos

- Usar siempre la misma inicial o el mismo nombre completo.
- No cambiar de `M` a `Milton` de un día para otro.
- Si un barbero no tiene comisión en el día, omitirlo de la lista (no escribir línea con `0`).

### Medios de pago

- `efectivo` se refiere a dinero en efectivo.
- `mp` se refiere a Mercado Pago (MPD y MPM combinados en un solo valor).
- Si hubo MPD y MPM por separado y se necesita desglosar, aclararlo en Observaciones.

### Secciones vacías

- Nunca omitir una sección. Si no hay datos, escribir `-`.
- `COMISIONES -` y `COMISIONES` con línea vacía no son lo mismo. Usar la primera forma.

---

## Ejemplo completo — día con actividad normal

```
CIERRE
fecha: 2026-05-22

COMISIONES
M | efectivo: 15000 | mp: 8500
F | efectivo: 12000 | mp: 0

EGRESOS
8500 | Insumos limpieza

RETIROS
Retiro semana | 15000

TARJETAS
35000

OBSERVACIONES
Seña confirmada para 23/05 con Pedro Gómez.
```

---

## Ejemplo completo — día con licencia médica

```
CIERRE
fecha: 2026-05-22

COMISIONES
M | efectivo: 18000 | mp: 12000
J | efectivo: 0 | mp: 43000

EGRESOS
-

RETIROS
-

TARJETAS
28000

OBSERVACIONES
J en licencia médica. Comisión de igual manera.
```

---

## Ejemplo completo — día sin comisiones, sin egresos, sin retiros

```
CIERRE
fecha: 2026-05-23

COMISIONES
-

EGRESOS
-

RETIROS
-

TARJETAS
12500

OBSERVACIONES
-
```

---

## Ejemplo completo — día con diferencia de caja

```
CIERRE
fecha: 2026-05-24

COMISIONES
M | efectivo: 20000 | mp: 10000

EGRESOS
15000 | Gasoil

RETIROS
-

TARJETAS
0

OBSERVACIONES
Diferencia de $500 en caja. Revisando turno de las 18hs. MPD cobrado pero no acreditó.
```

---

## Qué no hacer

- **No escribir montos incompletos:** `33` en vez de `33000` genera ambigüedad.
- **No omitir secciones:** si no hay comisiones, escribir `COMISIONES -`.
- **No usar nombres diferentes para el mismo barbero:** `M`, `Milton` y `Milt` en el mismo mensaje generan confusión.
- **No usar español inconsistente:** `Efectivo`, `efectivo` y `EFECTIVO` en el mismo mensaje.
- **No agregar secciones nuevas sin acordar:** este formato tiene 6 secciones. No agregar info que no corresponda a ninguna sección sin avisar previamente.

---

## Relación con el registro físico

El mensaje de WhatsApp se arma a partir de los totales calculados en el registro diario físico (`registro-diario-fisico.md`).

Pasos:
1. Completar el registro físico durante la jornada.
2. Calcular los totales al pie de la hoja.
3. Traducir los totales al formato del mensaje WhatsApp.
4. Enviar el mensaje a administración.
5. Archivar el registro físico.

---

## Qué no se implementa todavía

- **Automatización del envío:** el mensaje se arma y se envía manualmente.
- **Parsing automático:** no se implementa script que lea el mensaje y lo cargue en Sheets.
- **Validación automática:** no se implementa script que verifique consistencia entre mensaje y registro físico.

---

## Referencias

- Proceso de cierre diario: `../03_procesos/cierre-diario.md`
- Registro diario físico: `registro-diario-fisico.md`