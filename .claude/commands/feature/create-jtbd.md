---
argument-hint: [contexto-feature]
description: Crear análisis Job-to-be-Done para la feature actual
---

# Crear Análisis JTBD

Genera análisis Jobs To Be Done para la feature actual usando Product Owner y Feature Flow Manager.

**Uso**: `/create-jtbd [contexto-feature]`

## Qué Hace Este Comando

Orquesta dos agentes especializados:
1. **Product Owner** - Crea el documento JTBD aplicando framework completo
2. **Feature Flow Manager** - Valida y actualiza el estado de la feature

## Implementación

**Paso 1: Crear Documento JTBD**

Lanzar agente product-owner:

**Tarea**: "Crea análisis JTBD para la feature actual. Contexto: $ARGUMENTS"

**Paso 2: Actualizar Estado de Feature**

Lanzar agente feature-flow-manager:

**Tarea**: "Actualiza el estado de la feature actual tras completar JTBD. Marca stage 'jtbd' como completado y recomienda siguiente comando."

## Criterios de Éxito

- Product-owner crea JTBD.md exitosamente
- Feature-flow-manager actualiza .feature-state.json
- Stage "jtbd" marcado como completado
- Usuario recibe siguiente comando recomendado: /create-prd
