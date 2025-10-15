---
argument-hint: [contexto-adicional]
description: Organizar plan técnico por capacidades de usuario
---

# Organizar Plan Técnico

Reorganiza el plan técnico desde estructura de infraestructura a capacidades de usuario usando Feature Flow Manager.

**Uso**: `/organize-plan [contexto-adicional]`

## Qué Hace Este Comando

Orquesta agentes para reorganizar el plan técnico:
1. **Rails Architect**: Analiza dependencias técnicas y secuenciación
2. **Después**: Sintetiza plan organizado por capacidades
3. **Finalmente**: Feature Flow Manager valida y actualiza el estado

## Implementación

**Paso 1: Validar Prerequisitos**

Lee el plan técnico actual en `.contexts/.product/features/active/[feature-actual]/plan.md` y valida que existe.

Si no existe, informa al usuario: "Necesitas ejecutar /create-plan primero"

**Paso 2: Lanzar Rails Architect para Análisis de Dependencias**

Lanza el agente rails-architect:

**Tarea**:
```
Analiza dependencias técnicas y reorganiza por capacidades de usuario.

Contexto:
- Lee plan.md en .contexts/.product/features/active/[feature-actual]/plan.md
- Lee PRD.md en .contexts/.product/features/active/[feature-actual]/PRD.md
- Lee JTBD.md en .contexts/.product/features/active/[feature-actual]/JTBD.md (si existe)
- Contexto adicional del usuario: $ARGUMENTS

Objetivos:
1. Identificar capacidades de usuario desde el JTBD y PRD
2. Mapear tareas técnicas del plan.md a capacidades de usuario
3. Analizar dependencias entre tareas (qué debe completarse primero)
4. Identificar oportunidades de desarrollo en paralelo
5. Agrupar tareas por capacidad funcional (no por capa técnica)
6. Considerar patrones Rails de dependencia (modelo->servicio->controlador->vista)
7. Evaluar riesgos de bloqueo entre tareas

Devuelve:
- Lista de capacidades de usuario identificadas
- Mapeo de tareas a capacidades
- Análisis de dependencias entre tareas
- Secuencia recomendada de implementación
- Oportunidades de trabajo en paralelo
- Riesgos identificados por capacidad
```

**Paso 3: Esperar Resultado del Rails Architect**

El agente rails-architect analizará las dependencias y devolverá el análisis completo.

**Paso 4: Sintetizar Plan Organizado**

Con el análisis del rails-architect, crea el plan organizado.

Crea el archivo `.contexts/.product/features/active/[feature-actual]/plan-organized.md` con la siguiente estructura:

```markdown
# [Nombre Feature] - Plan Organizado por Capacidades

## Resumen de Reorganización
[Cómo se reorganizaron las tareas desde infraestructura a capacidades de usuario]

## Capacidad 1: [Nombre Capacidad de Usuario]

### Valor para el Usuario
[Qué Job To Be Done satisface, referenciando JTBD.md]

### Tareas de Implementación

#### Fundación (Completar Primero)
- [ ] [Tarea base de datos/modelo con ruta archivo]
- [ ] [Tarea setup servicio core]

#### Funcionalidad Core
- [ ] [Implementación lógica de negocio]
- [ ] [Creación endpoint API]
- [ ] [Setup job background si necesario]

#### Interfaz de Usuario
- [ ] [Creación controller y view frontend]
- [ ] [Features interactivas Hotwire/Stimulus]
- [ ] [Estilado CSS y diseño responsive]

#### Testing y Validación
- [ ] [Tests unitarios modelos y servicios]
- [ ] [Tests integración workflow completo]
- [ ] [Cobertura test multi-tenant]

### Dependencias
- **Internas**: [Otras capacidades de las que depende]
- **Externas**: [Servicios terceros o setup requerido]

### Factores de Riesgo
- [Bloqueos potenciales o desafíos para esta capacidad]

## Capacidad 2: [Nombre Capacidad de Usuario]
[Continuar misma estructura]

## Infraestructura de Soporte

### Requisitos Cross-Capacidad
- [ ] [Tareas que soportan múltiples capacidades]
- [ ] [Setup infraestructura necesaria entre features]
- [ ] [Framework seguridad y permisos]

### Framework Integración
- [ ] [Setup OAuth y autenticación]
- [ ] [Infraestructura webhooks]
- [ ] [Configuración servicio externo]

### Documentación y Deployment
- [ ] [Actualizaciones CLAUDE.md para nuevos patrones]
- [ ] [Actualizaciones documentación API]
- [ ] [Configuración entorno]
- [ ] [Planes deployment migración]

## Secuencia de Implementación Recomendada

### Fase 1: Fundación
[Qué capacidades implementar primero y por qué]

### Fase 2: Features Core
[Workflows usuarios primarios y sus dependencias]

### Fase 3: Capacidades Mejoradas
[Features secundarias y optimizaciones]

### Oportunidades de Desarrollo Paralelo
[Tareas que pueden trabajarse simultáneamente por diferentes desarrolladores]

---

*Plan organizado por capacidades de usuario mediante análisis de Rails Architect.*
*Total de tareas: [X]*
```

**Paso 5: Actualizar Estado con Feature Flow Manager**

Ahora que el plan está organizado, lanza el agente feature-flow-manager:

**Tarea**:
```
Actualiza el estado de la feature actual tras completar el plan organizado.

Acciones requeridas:
- Lee .contexts/.product/.feature-state.json actual
- Lee plan-organized.md y cuenta total de tareas (checkboxes [ ])
- Marca stage 'plan_organized' como completado
- Actualiza documento plan-organized.md como existente con timestamp
- Establece implementation.total_tasks = [número de tareas contadas]
- Establece implementation.completed_tasks = 0
- Establece workflow.current_stage = "planning"
- Establece workflow.next_recommended_command = "/implement-code"
- Actualiza updated_at con fecha actual
- Guarda .feature-state.json actualizado
- Muestra visualización de progreso al usuario
- Informa siguiente paso recomendado: /implement-code
```

## Criterios de Éxito

- Rails-architect analiza dependencias y reorganiza por capacidades
- Plan organizado sintetizado y guardado en plan-organized.md
- Tareas agrupadas por valor de usuario (no por capa técnica)
- Dependencias y secuencia de implementación claras
- Total de tareas contado correctamente
- Feature-flow-manager actualiza .feature-state.json
- Stage "plan_organized" marcado como completado
- Usuario recibe progreso visualizado y siguiente comando: /implement-code
