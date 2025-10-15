---
argument-hint: [filtro]
description: Listar todas las features con su estado
---

# Listar Features

Muestra lista de todas las features del pipeline con sus estados.

**Uso**: `/feature:list [filtro]`

**Ejemplos**:
- `/feature:list` - Todas las features
- `/feature:list active` - Solo activas
- `/feature:list archived` - Solo archivadas

## Qué Hace Este Comando

Delega al agente @feature-flow-manager para generar lista completa de features organizadas por estado.

## Implementación

Lanzar agente feature-flow-manager:

**Tarea**: "Lista todas las features del pipeline. Filtro: $ARGUMENTS"

El agente feature-flow-manager hará autónomamente:
- Cargar .feature-state.json completo
- Aplicar filtro si especificado (active/archived/trashed)
- Organizar features por estado del pipeline
- Mostrar información clave (nombre, estado, progreso)
- Indicar feature actual
- Calcular totales y métricas de pipeline

## Criterios de Éxito

- Feature-flow-manager lista features exitosamente
- Formato claro: nombre (estado) [progreso]
- Feature actual marcada con indicador ⚡
- Filtro aplicado correctamente si especificado
- Totales por estado mostrados
