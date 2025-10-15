---
argument-hint: <nombre-feature>
description: Mover feature a papelera
---

# Eliminar Feature

Mueve una feature a la papelera (eliminación soft, recuperable).

**Uso**: `/feature:trash <nombre-feature>`

**Ejemplo**: `/feature:trash user-authentication`

## Qué Hace Este Comando

Delega al agente @feature-flow-manager para mover la feature a papelera de forma recuperable.

## Implementación

Lanzar agente feature-flow-manager:

**Tarea**: "Mueve la feature a papelera: $ARGUMENTS"

El agente feature-flow-manager hará autónomamente:
- Validar que feature existe
- Confirmar si tiene trabajo significativo
- Mover directorio a features/trashed/
- Actualizar estado a "trashed" en .feature-state.json
- Registrar timestamp de eliminación
- Si era current_feature, cambiar a otra activa
- Generar confirmación de eliminación

## Criterios de Éxito

- Feature-flow-manager elimina (soft) exitosamente
- Directorio movido a features/trashed/
- Estado actualizado a "trashed"
- .feature-state.json refleja eliminación
- Usuario recibe confirmación
- Guía para restaurar si necesario: /feature:restore
