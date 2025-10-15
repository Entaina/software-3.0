---
argument-hint: <nombre-feature>
description: Cambiar la feature actual del pipeline
---

# Cambiar Feature Actual

Cambia la feature actual sobre la que operarán los comandos de desarrollo.

**Uso**: `/feature:switch <nombre-feature>`

**Ejemplo**: `/feature:switch user-authentication`

## Qué Hace Este Comando

Delega al agente @feature-flow-manager para cambiar la feature actual del contexto de trabajo.

## Implementación

Lanzar agente feature-flow-manager:

**Tarea**: "Cambia la feature actual del pipeline a: $ARGUMENTS"

El agente feature-flow-manager hará autónomamente:
- Validar que la feature existe y está activa
- Actualizar current_feature en .feature-state.json
- Actualizar archivo current-feature
- Actualizar timestamp de la feature
- Mostrar estado de la nueva feature actual
- Recomendar siguiente acción según progreso

## Criterios de Éxito

- Feature-flow-manager cambia feature exitosamente
- .feature-state.json actualizado con nuevo current_feature
- Archivo current-feature actualizado
- Usuario recibe estado de la nueva feature actual
- Siguiente comando recomendado según progreso
