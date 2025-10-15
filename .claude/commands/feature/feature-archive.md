---
argument-hint: <nombre-feature>
description: Archivar feature completada del pipeline
---

# Archivar Feature

Archiva una feature completada, moviéndola fuera del desarrollo activo.

**Uso**: `/feature-archive <nombre-feature>`

**Ejemplo**: `/feature-archive user-authentication`

## Qué Hace Este Comando

Delega al agente @feature-flow-manager para archivar la feature, documentar outcomes y actualizar métricas.

## Implementación

Lanzar agente feature-flow-manager:

**Tarea**: "Archiva la feature del pipeline: $ARGUMENTS"

El agente feature-flow-manager hará autónomamente:
- Validar que feature existe y puede archivarse
- Verificar criterios de completitud
- Crear ARCHIVE_SUMMARY.md con outcomes
- Mover directorio a features/archived/
- Actualizar estado a "archived" en .feature-state.json
- Documentar métricas finales (cycle time, lead time)
- Si era current_feature, cambiar a otra activa
- Generar reporte de archivo

## Criterios de Éxito

- Feature-flow-manager archiva exitosamente
- Directorio movido a features/archived/
- ARCHIVE_SUMMARY.md creado con learnings
- .feature-state.json actualizado
- Métricas del proyecto actualizadas
- Usuario recibe confirmación y summary
