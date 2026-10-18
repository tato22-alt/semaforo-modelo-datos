# El Semáforo — modelo de datos

Base de datos de un sistema de gestión para un taller de chapa y pintura: presupuestos,
clientes, vehículos y trabajos. **PostgreSQL sobre Supabase**, en uso real.

## En números

| | |
|---|---|
| Migraciones | 19, aplicadas en producción |
| Esquema | 4 tablas, 2 vistas, 5 funciones, 0 triggers |
| Verificación | 58 comprobaciones automáticas en una sola consulta, 58/58 en verde |
| Acceso | RLS activa y forzada; sin sesión no se lee ni se escribe nada |

## Tres decisiones que definen el diseño

- **Lo derivado no se guarda.** No hay columnas de total: los totales salen de una vista al
  leer. Un dato guardado dos veces termina diciendo dos cosas distintas.
- **La base es la API.** Supabase expone el esquema por REST; no hay servidor en el medio.
- **La numeración la reparte la base.** Una secuencia garantiza que dos personas cargando a la
  vez nunca saquen el mismo número de presupuesto.

## Cómo se trabajó

Spec-Driven Development: **spec → plan → tareas → migración**, y nada se migra sin una spec
aprobada. Cada feature tiene su carpeta en [`specs/`](./specs/), y los principios que mandan
sobre todo están en la [constitución](./.specify/memory/constitution.md).

| Feature | Estado |
|---|---|
| 001 Presupuesto | Cerrado y verificado con login real |
| 002 Numeración | Implementado |
| 003 Verificación del impreso | En pausa |
| 004 Chasis y observaciones | Implementado |
| 005 Detalle de mano de obra | Implementado |
| 006 Presupuestos pendientes | Implementado |
| 007 Borrador que no se pierde | Especificado |

## Dónde mirar

| | |
|---|---|
| [`supabase/migrations/`](./supabase/migrations/) | El esquema |
| [`specs/001-presupuesto/qa-001-verificacion.sql`](./specs/001-presupuesto/qa-001-verificacion.sql) | El QA: pegarlo en el editor SQL devuelve una fila por comprobación |
| [`docs/diccionario-datos.md`](./docs/diccionario-datos.md) | Qué guarda cada tabla y qué se deriva |

## Estado del repositorio

Congelado el 2026-10-07. El modelo siguió creciendo en un repositorio privado. Acá no hay
datos del taller: ni clientes, ni montos, ni credenciales.
