# Arquitectura de Stylos OS

## Propósito

Describir la arquitectura actual del sistema y su evolución prevista. Este documento se actualiza cuando cambia la arquitectura o se toman decisiones técnicas relevantes.

---

## Estado actual

Stylos OS funciona actualmente como un repositorio de documentación en Markdown, con Google Sheets como fuente principal de datos.

### Componentes

| Componente | Descripción | Estado |
|------------|-------------|--------|
| Repositorio Git | Documentación y estructura | Activo |
| Google Sheets | Datos económicos y operativos | Activo |
| Google Drive | Documentos compartidos | Activo |
| Fresha | Reservas y gestión de clientes | Activo (datos no integrados) |
| Markdown | Documentación, criterios, memoria | Activo |

### Flujo de información actual

```
Negocio → Cuaderno/WhatsApp/Fresha → Google Sheets → Análisis manual
Negocio → Google Drive → Documentos sueltos
Negocio → Memoria personal → (sin registro)
```

### Flujo objetivo (gradual)

```
Negocio → Fuentes varias → Stylos OS (docs + datos) → IA con contexto → Recomendación → Decisión humana → Registro en memoria
```

## Evolución prevista

No se implementa hasta que exista necesidad real. El orden sugerido es:

1. Documentación completa (etapa actual)
2. Exportación periódica de datos desde Sheets a `data/raw/`
3. Scripts de limpieza y validación en `scripts/`
4. Reportes automáticos simples
5. Integración con APIs (Fresha, Instagram) si se justifica
6. Base de datos local (SQLite primero, PostgreSQL después si se necesita)
7. Dashboard (Metabase u otro)
8. Automatizaciones (n8n u otro)

Cada paso requiere una decisión documentada en `docs/tecnico/decisiones-tecnicas/`.

## Decisiones técnicas

Ver `docs/tecnico/decisiones-tecnicas/`.
