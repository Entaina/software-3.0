---
argument-hint: <nombre-y-descripción>
description: Crear nueva feature con estructura y tracking
---

# Crear Feature

Crea una nueva feature con estructura de directorios y tracking inicial usando Feature Flow Manager.

**Uso**: `/feature:create <nombre-y-descripción>`

**Ejemplo**: `/feature:create user-authentication Sistema de autenticación con JWT`

## Qué Hace Este Comando

Delega al agente @feature-flow-manager para crear la estructura completa de una nueva feature en el pipeline.

## Implementación

Lanzar agente feature-flow-manager:

**Tarea**: "Crea nueva feature en el pipeline. Input del usuario: $ARGUMENTS"

El agente feature-flow-manager hará autónomamente:
- Parsear nombre y descripción de la feature
- Validar que no existe duplicado
- Crear estructura de directorios en `features/active/`
- Crear feature.md con información inicial
- Actualizar .feature-state.json con nueva feature
- Configurar estado inicial en "Backlog"

## Criterios de Éxito

- Feature-flow-manager crea estructura exitosamente
- Directorio creado en `features/active/[nombre-feature]/`
- feature.md generado con descripción y tracking
- .feature-state.json actualizado con nueva feature
- Usuario recibe guía: usar /feature:switch para activarla
