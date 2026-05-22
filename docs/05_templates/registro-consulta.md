# Registro de consulta

## Propósito

Plantilla para documentar una consulta importante realizada (a contador, asesor, IA, etc.) junto con la respuesta obtenida y cómo se verifició o aplicó.

---

## Estructura del registro

```
# Consulta: [título breve]

## Fecha
YYYY-MM-DD

## Pregunta
[Descripción de la consulta]

## Contexto
¿Qué situación motiva la consulta? ¿Qué información se tiene?

## Fuente
[Contador / Asesor / IA / Interno / Otro]

## Respuesta
[Descripción de la respuesta recibida]

## Verificación
[¿Se vérificó la respuesta? ¿Con qué método? ¿Se consultó otra fuente?]

## Aplicación
[¿Se aplicó la respuesta? ¿Cómo? ¿Resultó útil?]

## Notas
[Información adicional relevante]
```

---

## Instrucciones

- **Título:** breve y descriptivo.
- **Fuente:** indicar de dónde viene la respuesta: contador, asesor legal, IA, criterio interno, etc.
- **Verificación:** siempre indicar cómo se vérifier la respuesta antes de aplicarla. Si es información de IA, indicar que requiere verificación humana.
- **Aplicación:** documentar si se aplicó la respuesta y qué resultado tuvo.

---

## Ejemplo

```
# Consulta: ¿Cómo se declara el impuesto sobre los ingresos brutos en Argentina?

## Fecha

2026-05-20

## Pregunta

¿Cómo se calculan y declaran los ingresos brutos para una barbería en la provincia de Buenos Aires?

## Contexto

Estamos revisando los gastos del negocio y queremos entender la carga tributaria real. No queda claro si los ingresos brutos aplican a nuestro caso y cómo se calculan.

## Fuente

Contador (Lic. García, estudio contable XYZ)

## Respuesta

Los ingresos brutos en Buenos Aires se calculan sobre la facturación bruta con alícuota diferenciada para el sector servicios. La alícuota para barberías es aproximadamente 2.5%. Se paga mensualmente con declaración jurada. El contribuyente debe estar inscripto en ARBA.

## Verificación

Se solicitó confirmación por mail al contador con el archivo de la respuesta. Se recibió OK con firma digital del contador.

## Aplicación

Se incorporó el dato al modelo de gastos. El presupuesto mensual ahora incluye una línea de ingresos brutos estimada de 2.5% sobre la facturación.

## Notas

Revisar si hay exenciones por tamaño del emprendimiento. El contador mencionó quehay Regime Simplificado pero no aplica a SRL.
```

---

## Referencias

- Ver proceso de consultas: `../06_memoria/README.md`
- Si la consulta es a IA, guardar también el prompt usado en `../04_prompts/`