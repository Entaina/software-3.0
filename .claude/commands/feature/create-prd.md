---
argument-hint: [contexto-feature]
description: Crear Product Requirements Document para la feature actual
---

# Crear PRD

Genera Product Requirements Document para la feature actual usando Product Owner y Feature Flow Manager.

**Uso**: `/feature:create-prd [contexto-feature]`

## Qué Hace Este Comando

Orquesta dos agentes especializados:
1. **Product Owner** - Crea el PRD basándose en el análisis JTBD
2. **Feature Flow Manager** - Valida y actualiza el estado de la feature

## Implementación

**Paso 1: Crear Documento PRD**

Lanzar agente product-owner:

**Tarea**: "Crea PRD para la feature actual basándote en el JTBD existente. Contexto: $ARGUMENTS"

**Paso 2: Actualizar Estado de Feature**

Lanzar agente feature-flow-manager:

**Tarea**: "Actualiza el estado de la feature actual tras completar PRD. Marca stage 'prd' como completado y recomienda siguiente comando."

## Criterios de Éxito

- Product-owner crea PRD.md exitosamente
- Feature-flow-manager actualiza .feature-state.json
- Stage "prd" marcado como completado
- Usuario recibe siguiente comando recomendado: /feature:create-plan
