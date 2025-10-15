---
argument-hint: [contexto-adicional]
description: Crear plan técnico de implementación para la feature actual
---

# Crear Plan Técnico

Genera plan técnico de implementación orquestando agentes especializados y usando Feature Flow Manager.

**Uso**: `/feature:create-plan [contexto-adicional]`

## Qué Hace Este Comando

Orquesta múltiples agentes especializados para crear un plan técnico completo:
1. **En paralelo**: Rails Architect, Tailwind Specialist, Hotwire Specialist
2. **Después**: Sintetiza resultados en plan técnico
3. **Finalmente**: Feature Flow Manager valida y actualiza el estado

## Implementación

**Paso 1: Analizar PRD y Determinar Agentes Necesarios**

Lee el PRD de la feature actual en `.contexts/.product/features/active/[feature-actual]/PRD.md` y determina qué agentes especializados se necesitan:

- **Rails Architect**: Siempre necesario para arquitectura backend
- **Tailwind Specialist**: Si hay UI/frontend nuevo
- **Hotwire Specialist**: Si hay interactividad (formularios, modales, actualizaciones en tiempo real)

**Paso 2: Lanzar Agentes Especializados EN PARALELO**

Lanza todos los agentes necesarios EN PARALELO en un solo mensaje con múltiples invocaciones Task.

**IMPORTANTE**: Usa un solo mensaje con múltiples bloques <invoke name="Task"> para ejecutar en paralelo.

**Tarea para rails-architect**:
```
Analiza arquitectura Rails para la feature actual.

Contexto:
- Lee PRD en .contexts/.product/features/active/[feature-actual]/PRD.md
- Contexto adicional del usuario: $ARGUMENTS

Proporciona recomendaciones técnicas detalladas cubriendo:
- Decisiones arquitectónicas (modelos, servicios, controladores)
- Esquema de base de datos y migraciones
- Patrones Rails a seguir (Service Objects, concerns, etc.)
- Consideraciones multi-tenancy y aislamiento de datos
- Jobs en background si necesario (Solid Queue)
- Endpoints API y rutas REST
- Dependencias internas y externas
- Estrategia de testing (RSpec)
- Evaluación de riesgos técnicos

Devuelve un informe detallado con todas las decisiones arquitectónicas recomendadas.
```

**Tarea para tailwind-specialist** (si UI necesario):
```
Analiza necesidades de UI/frontend para la feature actual.

Contexto:
- Lee PRD en .contexts/.product/features/active/[feature-actual]/PRD.md
- Contexto adicional del usuario: $ARGUMENTS

Proporciona especificaciones de UI detalladas cubriendo:
- Componentes UI necesarios (botones, formularios, cards, etc.)
- Clases Tailwind CSS específicas para cada componente
- Layout y estructura responsive (mobile-first)
- Estados visuales (hover, focus, active, disabled, loading)
- Animaciones y transiciones
- Consideraciones de accesibilidad (ARIA, contraste, navegación)
- Integración con sistema de diseño existente

Devuelve un informe detallado con todas las especificaciones de UI.
```

**Tarea para hotwire-specialist** (si interactividad necesaria):
```
Analiza interactividad y actualizaciones en tiempo real para la feature actual.

Contexto:
- Lee PRD en .contexts/.product/features/active/[feature-actual]/PRD.md
- Contexto adicional del usuario: $ARGUMENTS

Proporciona especificaciones de interactividad detalladas cubriendo:
- Turbo Frames para actualizaciones parciales de página
- Turbo Streams para actualizaciones en tiempo real
- Stimulus controllers necesarios con actions y targets
- Estrategia de broadcasting con ActionCable (si tiempo real)
- Validaciones y feedback instantáneo al usuario
- Manejo de errores y estados de carga
- Optimistic UI updates donde corresponda

Devuelve un informe detallado con todas las especificaciones de interactividad.
```

**Paso 3: Esperar Resultados de Agentes**

Los agentes trabajarán en paralelo y devolverán sus hallazgos. Espera a que todos completen antes de continuar.

**Paso 4: Sintetizar Plan Técnico Completo**

Una vez que todos los agentes han devuelto sus informes, sintetiza un plan técnico completo integrando todos los hallazgos:

Crea el archivo `.contexts/.product/features/active/[feature-actual]/plan.md` con la siguiente estructura:

```markdown
# [Nombre Feature] - Plan Técnico de Implementación

## Resumen de la Feature
[Breve descripción conectando requisitos PRD con enfoque técnico]

## Visión General de Arquitectura

### Puntos de Integración del Sistema
[Cómo se integra con arquitectura Rails existente - del rails-architect]

### Consideraciones Multi-Tenant
[Aislamiento de cuentas, permisos, segregación de datos - del rails-architect]

### Stack Tecnológico Utilizado
[Rails 8.0, Jumpstart Pro, Hotwire, Tailwind, etc. - del rails-architect]

## Decisiones Técnicas Clave

### Framework y Elección de Patrones
[Patrones Service Objects, concerns, decorators - del rails-architect]

### Diseño de Base de Datos
[Esquema, migraciones, índices, performance - del rails-architect]

### Implementación Frontend
[Componentes UI, Tailwind classes, responsive - del tailwind-specialist]

### Interactividad y Tiempo Real
[Turbo Frames, Turbo Streams, Stimulus - del hotwire-specialist]

### Procesamiento en Background
[Solid Queue jobs, async operations - del rails-architect]

### Integración de Servicios Externos
[APIs, OAuth, webhooks - del rails-architect]

### Implementación de Seguridad
[Autenticación, autorización, protección de datos - del rails-architect]

## Dependencias y Asunciones

### Dependencias Internas
[Features existentes, componentes, servicios]

### Dependencias Externas
[Servicios terceros, APIs, librerías, infraestructura]

### Asunciones Técnicas
[Capacidad del sistema, carga de usuarios, volumen de datos]

## Checklist de Implementación

### Implementación Backend
- [ ] [Tarea específica con ruta de archivo - del rails-architect]
- [ ] [Migración y modelo - del rails-architect]
- [ ] [Service Object para lógica de negocio - del rails-architect]
- [ ] [Endpoint API REST - del rails-architect]
- [ ] [Job background Solid Queue - del rails-architect]

### Implementación Frontend
- [ ] [View template Rails - del tailwind-specialist]
- [ ] [Componente UI con Tailwind - del tailwind-specialist]
- [ ] [Stimulus controller - del hotwire-specialist]
- [ ] [Turbo Frame/Stream - del hotwire-specialist]
- [ ] [Responsividad móvil - del tailwind-specialist]

### Implementación Testing
- [ ] [Test RSpec modelo - del rails-architect]
- [ ] [Test RSpec servicio - del rails-architect]
- [ ] [Test integración controller - del rails-architect]
- [ ] [System test flujo completo - del rails-architect]
- [ ] [Test multi-tenant - del rails-architect]

### Documentación y Deployment
- [ ] [Actualizar CLAUDE.md]
- [ ] [Documentación API]
- [ ] [Variables de entorno]
- [ ] [Plan deployment migración]

## Evaluación de Riesgos y Mitigación

### Riesgos Técnicos
[Desafíos potenciales y estrategias de mitigación - de todos los agentes]

### Riesgos de Rendimiento
[Escalabilidad y optimización - del rails-architect]

### Riesgos de Seguridad
[Consideraciones de seguridad - del rails-architect]

### Riesgos de Integración
[Dependencias externas y planes de contingencia - del rails-architect]

## Fases de Implementación

### Fase 1: Fundación Core
[Base de datos, modelos, servicios básicos]

### Fase 2: Lógica de Negocio
[Service Objects, endpoints API, jobs]

### Fase 3: Interfaz de Usuario
[Views, componentes UI, interactividad]

### Fase 4: Integración y Pulido
[Integraciones externas, testing, documentación]

---

*Plan técnico creado mediante análisis colaborativo de agentes especializados: Rails Architect, Tailwind Specialist, Hotwire Specialist.*
```

**Paso 5: Actualizar Estado con Feature Flow Manager**

Ahora que el plan está completo, lanza el agente feature-flow-manager:

**Tarea**:
```
Actualiza el estado de la feature actual tras completar el plan técnico.

Acciones requeridas:
- Lee .contexts/.product/.feature-state.json actual
- Marca stage 'plan' como completado
- Actualiza documento plan.md como existente con timestamp
- Establece workflow.current_stage = "planning"
- Establece workflow.next_recommended_command = "/feature:organize-plan"
- Actualiza updated_at con fecha actual
- Guarda .feature-state.json actualizado
- Muestra visualización de progreso al usuario
- Informa siguiente paso recomendado: /feature:organize-plan
```

## Criterios de Éxito

- Agentes especializados ejecutados en paralelo exitosamente
- Rails-architect proporciona arquitectura backend completa
- Tailwind-specialist proporciona especificaciones UI (si necesario)
- Hotwire-specialist proporciona diseño de interactividad (si necesario)
- Plan técnico completo sintetizado y guardado en plan.md
- Feature-flow-manager actualiza .feature-state.json
- Stage "plan" marcado como completado
- Usuario recibe progreso visualizado y siguiente comando: /feature:organize-plan
