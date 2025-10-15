---
argument-hint: [nombre-feature]
description: Mostrar estado detallado de una feature
---

# Estado de Feature

Muestra estado detallado y progreso de una feature en el pipeline.

**Uso**: `/feature-status [nombre-feature]`

**Ejemplos**:
- `/feature-status` - Estado de la feature actual
- `/feature-status user-auth` - Estado de feature específica

## Qué Hace Este Comando

Delega al agente @feature-flow-manager para generar reporte completo de estado, progreso, blockers y métricas de la feature.

## Implementación

Lanzar agente feature-flow-manager:

**Tarea**: "Genera reporte de estado completo para feature. Target: $ARGUMENTS"

El agente feature-flow-manager hará autónomamente:
- Determinar feature target (argumento o current-feature)
- Cargar estado desde .feature-state.json
- Analizar todos los documentos de la feature
- Calcular progreso y tiempo en cada estado
- Identificar blockers activos
- Generar reporte con visualización de progreso
- Recomendar siguiente acción

## Criterios de Éxito

- Feature-flow-manager completa análisis exitosamente
- Usuario recibe reporte detallado de estado
- Progreso mostrado con visualización clara (% y etapas)
- Blockers identificados si existen
- Siguiente acción recomendada proporcionada
