---
argument-hint: <nombre-feature>
description: Restaurar feature archivada o eliminada
---

# Restaurar Feature

Restaura una feature archivada o eliminada volviéndola al estado activo.

**Uso**: `/feature-restore <nombre-feature>`

**Ejemplo**: `/feature-restore user-authentication`

## Qué Hace Este Comando

Delega al agente @feature-flow-manager para restaurar la feature al pipeline activo.

## Implementación

Lanzar agente feature-flow-manager:

**Tarea**: "Restaura la feature al pipeline activo: $ARGUMENTS"

El agente feature-flow-manager hará autónomamente:
- Buscar feature en archived/ o trashed/
- Validar que puede restaurarse
- Mover directorio a features/active/
- Actualizar estado a "active" en .feature-state.json
- Actualizar timestamps (restored_at)
- Mostrar estado de la feature restaurada
- Recomendar siguiente acción según progreso previo

## Criterios de Éxito

- Feature-flow-manager restaura exitosamente
- Directorio movido a features/active/
- Estado actualizado a "active"
- .feature-state.json refleja restauración
- Usuario recibe estado actual de feature
- Siguiente acción recomendada
