---
argument-hint: [contexto-adicional]
description: Implementar siguiente tarea del plan organizado
---

# Implementar Código

Implementa la siguiente tarea del plan organizado orquestando agentes especializados según necesidades.

**Uso**: `/feature:implement-code [contexto-adicional]`

## Qué Hace Este Comando

Orquesta agentes especializados para implementar la siguiente tarea:
1. **Identifica** siguiente tarea pendiente en plan-organized.md
2. **En paralelo** (si necesario): Rails Architect, Tailwind Specialist, Hotwire Specialist
3. **Después**: Implementa código basándose en análisis de agentes
4. **Finalmente**: Feature Flow Manager actualiza progreso

## Implementación

**Paso 1: Identificar Siguiente Tarea**

Lee `.contexts/.product/features/active/[feature-actual]/plan-organized.md` y:
- Encuentra la primera tarea con checkbox `[ ]` (no completada)
- Verifica que sus dependencias previas estén completas `[x]`
- Identifica qué capacidad de usuario pertenece la tarea
- Lee contexto de la capacidad (valor usuario, dependencias, riesgos)

Si todas las tareas están completadas `[x]`, informa: "¡Todas las tareas están completas! Ejecuta /feature:archive para archivar la feature."

**Paso 2: Analizar Complejidad de la Tarea**

Basándose en la descripción de la tarea, determina qué agentes especializados se necesitan:

**Tarea Backend (modelos, servicios, jobs, API)**:
- Rails Architect: Siempre necesario

**Tarea Frontend (views, componentes UI)**:
- Rails Architect: Para estructura Rails
- Tailwind Specialist: Para implementación UI

**Tarea Interactividad (Turbo, Stimulus, tiempo real)**:
- Rails Architect: Para endpoints backend
- Hotwire Specialist: Para interactividad
- Tailwind Specialist: Para estados visuales (si necesario)

**Tarea Testing**:
- Rails Architect: Para estrategia y patrones de testing

**Paso 3: Lanzar Agentes Especializados EN PARALELO (si múltiples)**

Si necesitas múltiples agentes, lánzalos EN PARALELO en un solo mensaje con múltiples invocaciones Task.

**IMPORTANTE**: Usa un solo mensaje con múltiples bloques <invoke name="Task"> para ejecutar en paralelo.

**Tarea para rails-architect** (siempre para implementación):
```
Implementa la siguiente tarea del plan organizado.

Contexto:
- Tarea a implementar: [descripción de la tarea desde plan-organized.md]
- Capacidad de usuario: [nombre de la capacidad]
- Lee plan-organized.md en .contexts/.product/features/active/[feature-actual]/plan-organized.md
- Lee PRD.md en .contexts/.product/features/active/[feature-actual]/PRD.md
- Contexto adicional del usuario: $ARGUMENTS

Implementa siguiendo:
- Patrones Rails establecidos en el proyecto
- Principios SOLID y código limpio
- Consideraciones multi-tenancy
- Convenciones de testing RSpec
- Mejores prácticas de seguridad

Devuelve:
- Código completo a crear/modificar
- Rutas de archivos específicas
- Explicación de decisiones arquitectónicas
- Tests necesarios
- Próximos pasos tras completar esta tarea
```

**Tarea para tailwind-specialist** (si UI necesaria):
```
Implementa UI para la siguiente tarea del plan organizado.

Contexto:
- Tarea a implementar: [descripción de la tarea]
- Lee plan-organized.md en .contexts/.product/features/active/[feature-actual]/plan-organized.md
- Lee sistema de diseño en .contexts/design-system/
- Contexto adicional del usuario: $ARGUMENTS

Implementa:
- Componentes UI con Tailwind CSS
- Clases específicas del sistema de diseño
- Estados visuales (hover, focus, disabled, loading)
- Diseño responsive mobile-first
- Consideraciones de accesibilidad

Devuelve:
- Código HTML/ERB completo
- Clases Tailwind específicas
- Variantes de estados
- Código CSS custom si absolutamente necesario
```

**Tarea para hotwire-specialist** (si interactividad necesaria):
```
Implementa interactividad para la siguiente tarea del plan organizado.

Contexto:
- Tarea a implementar: [descripción de la tarea]
- Lee plan-organized.md en .contexts/.product/features/active/[feature-actual]/plan-organized.md
- Contexto adicional del usuario: $ARGUMENTS

Implementa:
- Turbo Frames para actualizaciones parciales
- Turbo Streams para actualizaciones tiempo real
- Stimulus controllers con actions y targets
- Broadcasting ActionCable si necesario
- Manejo de errores y estados de carga

Devuelve:
- Código Stimulus JavaScript completo
- Configuración Turbo Frames/Streams
- Código backend para broadcasts si necesario
- Manejo de edge cases
```

**Paso 4: Esperar Resultados de Agentes**

Los agentes trabajarán en paralelo (si múltiples) y devolverán sus hallazgos. Espera a que todos completen.

**Paso 5: Implementar Código Integrando Hallazgos**

Con los informes de los agentes, implementa el código:

1. **Crear/Modificar archivos** según recomendaciones de agentes
2. **Integrar hallazgos**:
   - Arquitectura backend del rails-architect
   - UI del tailwind-specialist
   - Interactividad del hotwire-specialist
3. **Seguir convenciones** del proyecto
4. **Crear tests** según estrategia del rails-architect
5. **Validar implementación** manualmente si es posible

**Paso 6: Actualizar Plan Organizado**

Marca la tarea como completada en plan-organized.md:
- Cambia `[ ]` a `[x]` para la tarea implementada
- Añade nota si hay decisiones importantes: `[x] Tarea completada (nota: decisión X tomada)`

**Paso 7: Actualizar Estado con Feature Flow Manager**

Ahora que la tarea está completa, lanza el agente feature-flow-manager:

**Tarea**:
```
Actualiza el estado de la feature actual tras completar una tarea de implementación.

Acciones requeridas:
- Lee .contexts/.product/.feature-state.json actual
- Lee plan-organized.md y cuenta tareas completadas [x]
- Incrementa implementation.completed_tasks en 1
- Actualiza implementation.last_implementation con timestamp actual
- Actualiza documento plan-organized.md.last_modified con timestamp
- Si completed_tasks == total_tasks:
  - Establece workflow.current_stage = "complete"
  - Establece workflow.next_recommended_command = "/feature:archive [nombre-feature]"
- Si completed_tasks < total_tasks:
  - Establece workflow.current_stage = "development"
  - Establece workflow.next_recommended_command = "/feature:implement-code"
- Actualiza updated_at con fecha actual
- Guarda .feature-state.json actualizado
- Muestra visualización de progreso al usuario con:
  - Progreso: [█████░░░] X% (completed/total tareas)
  - Última tarea completada: [descripción]
  - Siguiente tarea pendiente: [descripción] (si existe)
- Informa siguiente paso recomendado
```

## Criterios de Éxito

- Siguiente tarea identificada correctamente desde plan-organized.md
- Agentes especializados ejecutados según complejidad de tarea
- Rails-architect proporciona implementación backend (siempre)
- Tailwind-specialist proporciona implementación UI (si necesario)
- Hotwire-specialist proporciona interactividad (si necesario)
- Código implementado correctamente con tests
- Tarea marcada como completada [x] en plan-organized.md
- Feature-flow-manager actualiza .feature-state.json
- Contador de tareas incrementado
- Usuario recibe progreso visualizado y siguiente acción
