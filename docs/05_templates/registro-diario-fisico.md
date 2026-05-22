# Registro diario físico — Template

## Propósito

Plantilla para el registro físico de la jornada diaria de caja en Stylo's Barber.

**Formato:** A4 apaisado (horizontal), optimizado para impresión en papel o uso en pantalla.
**Uso previsto:** Recepción. Registro manual durante la jornada.
**No reemplaza:** Fresha como CRM, ni la carga en Sheets.

---

## Instrucciones de uso

1. Imprimir una copia al inicio de cada jornada o mantener una en pantalla.
2. Cada vez que ocurre un movimiento (servicio, egreso, comisión, retiro, ajuste, seña), registrar una fila.
3. Completar todas las columnas aplicables. Las columnas Hora y Observación son opcionales según el movimiento.
4. Al cierre de la jornada, calcular los totales al pie.
5. Verificar que la caja contada coincida con la caja esperada. Si hay diferencia, documentarla en Observaciones.
6. Usar los totales para armar el mensaje de WhatsApp de cierre (ver `cierre-diario-whatsapp.md`).
7. Archivar la hoja como respaldo físico.

---

## Estructura de la hoja

### Encabezado

```
STYLO'S BARBER — REGISTRO DIARIO DE CAJA
Fecha: __ / __ / ____         Periodo: ___________
```

### Columnas

| N° | Hora | Tipo | Cliente / Detalle | Barbero | Servicio | Medio de pago | Ingreso | Salida | Observación |
|----|------|------|-------------------|---------|----------|---------------|---------|--------|-------------|
| 1 | | | | | | | | | |
| 2 | | | | | | | | | |
| 3 | | | | | | | | | |
| 4 | | | | | | | | | |
| 5 | | | | | | | | | |
| 6 | | | | | | | | | |
| 7 | | | | | | | | | |
| 8 | | | | | | | | | |
| 9 | | | | | | | | | |
| 10 | | | | | | | | | |
| 11 | | | | | | | | | |
| 12 | | | | | | | | | |
| 13 | | | | | | | | | |
| 14 | | | | | | | | | |
| 15 | | | | | | | | | |

*(Agregar filas según necesidad)*

### Totales al pie

```
--- TOTALES ---

INGRESOS
Efectivo:         $ ____________
MPD:              $ ____________
MPM:              $ ____________
Tarjeta:          $ ____________
Transferencia:    $ ____________
─────────────────────────────
TOTAL INGRESOS:   $ ____________

SALIDAS
Egresos:          $ ____________
Comisiones:       $ ____________
Retiros:          $ ____________
─────────────────────────────
TOTAL SALIDAS:    $ ____________

CAJA
Caja final esperada:  $ ____________
Caja final contada:   $ ____________
Diferencia:            $ ____________

OBSERVACIONES:
___________________________________________________________________
___________________________________________________________________
```

---

## Valores válidos

### Tipo

| Valor | Uso para |
|-------|---------|
| Servicio | Pago por corte, barba, tratamiento u otro servicio |
| Producto | Venta de producto (pomada, aceite, etc.) |
| Egreso | Gasto extraordinario del local |
| Comisión | Pago de comisión a barbero |
| Retiro | Retiro de dinero de caja por socio/responsable |
| Ajuste | Corrección de monto anterior (diferencia, devolución) |
| Seña | Anticipo por servicio futuro confirmado |
| Otro | Movimiento que no corresponde a las categorías anteriores |

### Medio de pago

| Valor | Significado |
|-------|-------------|
| Efectivo | Billetes y monedas |
| MPD | Mercado Pago débito / cuotas |
| MPM | Mercado Pago mercado / monedero / link |
| Tarjeta | Tarjeta de crédito o débito (no MP) |
| Transferencia | Transferencia bancaria u otro medio |
| Otro | Medio no contemplado |

**Nota sobre Transferencia:** El modelo actual de Sheets (Caja_diaria) no incluye columna para Transferencia. Si se registra una transferencia, aclararla en la columna Observación y en el mensaje de WhatsApp. No agrupar bajo otro medio.

### Nombres de barberos

Usar siempre el mismo formato de nombre. Ejemplos:
- `M` para Milton
- `F` para Facundo
- `J` para Javier

No cambiar el formato de un día para otro. Si hay dudas, aclararlo en Observación.

---

## Ejemplos de registro

### Servicio cobrado en efectivo

```
| 1 | 10:30 | Servicio | Juan Pérez | M | Corte | Efectivo | 3000 | — | — |
```

### Servicio cobrado por MPD

```
| 2 | 11:00 | Servicio | Carlos Ruiz | F | Corte+Barba | MPD | 5500 | — | — |
```

### Egreso extraordinario

```
| 3 | — | Egreso | Insumos limpieza | — | — | Efectivo | — | 8500 | — |
```

### Pago de comisión

```
| 4 | — | Comisión | — | M | — | Efectivo | — | 12000 | — |
```

### Retiro de socio

```
| 5 | — | Retiro | — | — | — | Efectivo | — | 15000 | Retiro semana |
```

### Ajuste por diferencia

```
| 6 | — | Ajuste | — | — | — | — | — | 500 | Diferencia MPD |
```

### Seña por turno futuro

```
| 7 | 14:00 | Seña | Pedro Gómez | F | Corte | Efectivo | 2000 | — | Confirmó para 22/05 |
```

### Día con licencia médica (comisión sin servicio)

```
| 8 | — | Comisión | Licencia médica | J | — | MPD | — | 43000 | — |
```

---

## Reglas de completado

- **Ingreso y Salida:** completar solo uno, según el Tipo. El otro queda vacío.
- **Hora:** opcional. Omitir en días de bajo movimiento o si no es relevante.
- **Cliente / Detalle:** obligatorio para Servicios, Señas y Productos. Opcional para otros tipos.
- **Barbero:** obligatorio para Servicios y Comisiones. Para Egresos, Retiros y Ajustes puede quedar vacío si el movimiento no es atribuible a un barbero específico.
- **Observación:** usar para situaciones especiales: licencias, señas confirmadas, ajustes, diferencias de caja, contextos importantes.
- **Montos:** escribir el monto completo. No usar abreviaturas (ej: escribir `3000` en vez de `3` o `3mil`).

---

## Notas para impresión

- Imprimir en formato A4 horizontal.
- Si se imprime en hojas recicladas o doble faz, asegurar que la tabla sea legible.
- Mantener copias en blanco en un folder accessible para recepción.
- El formato también puede usarse en pantalla con una tabla digital (Google Sheets, Excel, etc.) manteniendo las mismas columnas.