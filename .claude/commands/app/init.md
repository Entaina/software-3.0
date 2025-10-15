---
argument-hint: <descripción-aplicación>
description: Inicializar una nueva aplicación Rails con decisiones colaborativas de todos los agentes especializados
---

# Inicializar Aplicación - Flujo Colaborativo Multi-Agente

Inicializa una nueva aplicación Rails con orientación coordinada del Product Owner, Rails Architect, Tailwind Specialist y Hotwire Specialist trabajando colaborativamente.

**Uso**: `/app:init <descripción-aplicación>`

**Ejemplo**: `/app:init "Sistema CRM para gestionar leads de ventas con tablero kanban e integración de email"`

## Qué hace este comando

Este comando orquesta un proceso completo de inicialización de aplicación donde varios agentes especializados colaboran para tomar decisiones informadas sobre tu aplicación:

1. **Crear aplicación Rails vacía** en la carpeta actual
2. **Inicializar CLAUDE.md** con instrucciones para usar context-engineer y agentes
3. **Feature Flow Manager** - Crea la primera tarea para versión inicial
4. **Product Owner** - Define la funcionalidad mínima viable
5. **Agentes técnicos en paralelo** - Rails Architect, Tailwind Specialist y Hotwire Specialist planifican la implementación
6. **Ejecutar el plan** - Implementa lo que los agentes han decidido
7. **Context Engineer** - Actualiza los contextos con todas las decisiones tomadas

## Implementación

### Paso 1: Crear Aplicación Rails Vacía

Primero, verifica si git ya está inicializado:

```bash
if [[ -d ".git" ]]; then
  echo "Git ya está inicializado"
  rails new . --css=tailwind --database=sqlite3 --skip-git
else
  echo "Git no está inicializado, Rails lo inicializará"
  rails new . --css=tailwind --database=sqlite3
fi
```

**Notas**:
- Si `.git` existe, usamos `--skip-git` para no crear un nuevo repositorio git
- Si no existe, Rails inicializará git automáticamente
- Si hay archivos existentes, Rails preguntará antes de sobrescribir. Acepta sobrescribir solo si es apropiado.
- La aplicación rails se tiene que crear en el current folder

### Paso 2: Inicializar CLAUDE.md

Crea el archivo `CLAUDE.md` en la raíz del proyecto con las siguientes instrucciones:

```markdown
# CLAUDE.md

Este archivo proporciona orientación a Claude Code al trabajar con código en este repositorio.

## IMPORTANTE: Antes de Ejecutar Cualquier Tarea

**SIEMPRE** llama primero al agente `context-engineer` para cargar el contexto apropiado antes de ejecutar cualquier tarea:

Usa el agente context-engineer con la descripción de la tarea para:
- Cargar contexto relevante de .contexts/
- Identificar ADRs aplicables
- Revisar especificaciones relacionadas
- Cargar convenciones del proyecto
- Proporcionar recomendaciones de implementación

## Uso de Agentes Especializados

Según la tarea pedida por el usuario, asegúrate de llamar a los agentes pertinentes:

### Product Owner (product-owner)
Úsalo cuando:
- Se necesite definir QUÉ construir (no CÓMO)
- Para crear PRDs o especificaciones JTBD
- Al priorizar características o decidir qué construir
- Para validar métricas post-lanzamiento
- Cuando haya que decir NO a características innecesarias

### Rails Architect (rails-architect)
Úsalo cuando:
- Se diseñe arquitectura de nuevas características
- Haya decisiones arquitectónicas (Service Objects, patrones, etc.)
- Se revise código contra principios SOLID/KISS/YAGNI
- Se refactorice código complejo
- Se necesiten decisiones sobre REST vs rutas personalizadas

### Tailwind Specialist (tailwind-specialist)
Úsalo cuando:
- Se implementen componentes UI con Tailwind CSS
- Se configure Tailwind en el proyecto
- Se optimice rendimiento de bundles CSS
- Se implemente dark mode o temas
- Haya problemas de estilos con Tailwind

### Hotwire Specialist (hotwire-specialist)
Úsalo cuando:
- Se implementen características interactivas
- Se necesite edición inline, modales, actualizaciones en tiempo real
- Haya que decidir entre Turbo Frames, Streams o Stimulus
- Se debuggeen problemas de Turbo o Stimulus
- Se implementen broadcasts con ActionCable

### Context Engineer (context-engineer)
Úsalo:
- **SIEMPRE al inicio de cualquier tarea** (obligatorio)
- Al refactorizar o planificar implementaciones
- Para recuperar decisiones arquitectónicas pasadas
- Al actualizar contexto tras cambios importantes
- Cuando se necesite onboarding en el proyecto

### Feature Flow Manager (feature-flow-manager)
Úsalo cuando:
- Se revise el estado del pipeline de características
- Se actualice el estado de características (Discovery → Development → Review → Production)
- Se reporten blockers o métricas de flujo
- Se archiven características completadas
- Se necesite capacidad de planificación

## Descripción del Proyecto

$ARGUMENTS

## Stack Tecnológico

- **Framework**: Ruby on Rails 8
- **CSS**: Tailwind CSS
- **JavaScript**: Hotwire (Turbo + Stimulus)
- **Base de datos**: SQLite3 (desarrollo y producción simple)
```

Guarda este archivo como `CLAUDE.md` en la raíz del proyecto.

### Paso 3: Crear Primera Tarea con Feature Flow Manager

Llama al agente `feature-flow-manager` para crear la primera característica:

**Tarea**: "Crear característica v1.0-mvp para: $ARGUMENTS"

El Feature Flow Manager debe:
- Crear la característica "v1.0-mvp" en estado Discovery
- Establecer objetivo: Crear la primera versión funcional mínima
- Documentar en `.product/features/v1.0-mvp/`
- Preparar para la fase de definición con Product Owner

**Espera a que el Feature Flow Manager complete antes de continuar.**

### Paso 4: Definir Funcionalidad Mínima con Product Owner

Llama al agente `product-owner` para especificar el MVP:

**Tarea**: "Define la funcionalidad mínima viable para: $ARGUMENTS"

El Product Owner debe:
- Realizar análisis JTBD (Jobs To Be Done)
- Identificar problemas core que la app resuelve
- Definir características must-have vs nice-to-have
- Crear PRD lean con métricas de éxito
- Recomendar alcance MVP (lo MÍNIMO para validar)
- Documentar qué NO incluir en v1.0

**Output esperado**:
- `.product/features/v1.0-mvp/jtbd.md`
- `.product/features/v1.0-mvp/prd.md`

**Espera a que el Product Owner complete antes de continuar.**

### Paso 5: Planificación Técnica en Paralelo

Lanza **en paralelo** (en un solo mensaje) los siguientes 3 agentes especializados con la información del PRD:

#### 5.1 Rails Architect

**Tarea**: "Diseña la arquitectura Rails para: $ARGUMENTS (basado en el PRD y sistema de diseño)"

Debe:
- Diseñar esquema de base de datos (modelos, asociaciones, validaciones)
- Planificar recursos REST y rutas
- Identificar qué necesita Service Objects (operaciones complejas)
- Diseñar estrategia de autenticación/autorización si aplica
- Recomendar gemas necesarias
- Definir estructura de carpetas y namespaces
- Aplicar principios SOLID
- Planificar estrategia de testing

**Output**: Documento de arquitectura con modelos, rutas y decisiones técnicas

#### 5.2 Tailwind Specialist

**Tarea**: "Configura Tailwind CSS para: $ARGUMENTS (basado en el sistema de diseño)"

Debe:
- Configurar `tailwind.config.js` con design tokens
- Mapear colores del sistema de diseño a paleta Tailwind
- Configurar escala de espaciado personalizada si es necesaria
- Configurar rutas de contenido para Rails
- Recomendar plugins Tailwind (@tailwindcss/forms, typography, etc.)
- Configurar dark mode si es necesario
- Definir utilities de componentes para patrones reutilizables
- Planificar breakpoints responsive

**Output**: `tailwind.config.js` completo e instrucciones de setup

#### 5.3 Hotwire Specialist

**Tarea**: "Planifica las características interactivas para: $ARGUMENTS (basado en PRD y arquitectura)"

Debe:
- Identificar características que requieren Turbo Frames (edición inline, modales)
- Identificar características que requieren Turbo Streams (actualizaciones en tiempo real)
- Planificar controllers Stimulus para interacciones client-side
- Diseñar broadcasts ActionCable si son necesarios
- Planificar navegación con Turbo Drive
- Recomendar patrones Hotwire para cada característica
- Planificar estrategia de progressive enhancement

**Output**: Plan de implementación Hotwire con patrones específicos

**IMPORTANTE**: Estos 3 agentes deben ejecutarse en PARALELO usando múltiples llamadas al tool Task en un solo mensaje.

**Espera a que TODOS los agentes técnicos completen antes de continuar.**

### Paso 6: Ejecutar el Plan de Implementación

Con toda la información de los agentes:

1. **Genera el código base**:
   - Genera modelos: `rails g model ModelName field:type`
   - Ejecuta migraciones: `rails db:migrate`
   - Genera controllers: `rails g controller ControllerName actions`
   - Configura rutas en `config/routes.rb`

2. **Implementa el sistema de diseño**:
   - Aplica configuración de `tailwind.config.js`
   - Crea helpers de diseño en `app/helpers/design_system_helper.rb`
   - Implementa layout base con navegación y estilos

3. **Implementa vistas con Tailwind**:
   - Crea vistas siguiendo especificaciones del Tailwind Specialist
   - Aplica clases Tailwind según especificaciones
   - Implementa componentes reutilizables

4. **Implementa interactividad con Hotwire**:
   - Configura Turbo Frames donde especificado
   - Implementa Turbo Streams para actualizaciones en tiempo real
   - Crea Stimulus controllers según el plan
   - Configura ActionCable si es necesario

5. **Validaciones y lógica de negocio**:
   - Añade validaciones a modelos
   - Implementa Service Objects para operaciones complejas
   - Añade autenticación/autorización si aplica

6. **Crea datos de ejemplo**:
   - Actualiza `db/seeds.rb` con datos de prueba
   - Ejecuta: `rails db:seed`

### Paso 7: Actualizar Contextos con Context Engineer

Llama al agente `context-engineer` para documentar todo:

**Tarea**: "Actualiza contextos basándote en la aplicación Rails creada: $ARGUMENTS"

El Context Engineer debe:
- Crear ADRs para decisiones arquitectónicas tomadas
- Documentar convenciones de código establecidas
- Guardar configuraciones importantes
- Documentar sistema de diseño
- Crear troubleshooting común
- Generar resumen de contexto

**Output esperado**:
- ADRs en `.contexts/adrs/`
- Convenciones en `.contexts/conventions/`
- Configuración en `.contexts/config/`
- Resumen en `.contexts/SUMMARY.md`

### Paso 8: Reporte Final al Usuario

Presenta un resumen completo al usuario:

```markdown
# ✅ Aplicación Inicializada: "$ARGUMENTS"

## 🎯 Decisiones del Product Owner
- **JTBD Core**: [resumen]
- **Características MVP**: [lista]
- **Métricas de Éxito**: [métricas]
- **Excluido de v1.0**: [lo que NO se incluye]

## 🎨 Sistema de Diseño
- **Color primario**: [color]
- **Tipografía**: [fuentes]
- **Estilo de componentes**: [descripción]
- **Documentado en**: `.design-system/visual-guidelines.md`

## 🏗️ Arquitectura Rails
- **Modelos core**: [lista]
- **Patrones usados**: [Service Objects/etc]
- **Autenticación**: [estrategia]
- **Base de datos**: SQLite3

## 💅 Configuración Tailwind
- **Config**: `tailwind.config.js` listo
- **Plugins**: [lista]
- **Utilities personalizadas**: [si hay]

## ⚡ Plan Hotwire
- **Turbo Frames**: [características que los usan]
- **Turbo Streams**: [características que los usan]
- **Stimulus Controllers**: [controllers necesarios]

## 📁 Estructura Creada
```
.
├── app/                    # Aplicación Rails
├── config/                 # Configuración
├── db/                     # Base de datos y migraciones
├── .contexts/              # Documentación de contexto
│   ├── adrs/              # Decisiones arquitectónicas
│   ├── specs/             # Especificaciones
│   └── conventions/       # Convenciones de código
├── .product/              # Gestión de producto
│   └── features/
│       └── v1.0-mvp/      # Primera versión
└── CLAUDE.md              # Guía para Claude Code
```

## 🚀 Próximos Pasos

1. **Revisar documentación**:
   - PRD: `.product/features/v1.0-mvp/prd.md`
   - Arquitectura: Ver ADRs en `.contexts/adrs/`
   - Diseño: `.design-system/visual-guidelines.md`

2. **Iniciar desarrollo**:
   ```bash
   bin/dev  # Arranca servidor con Tailwind watch
   ```

3. **Crear datos de prueba**:
   ```bash
   rails db:seed
   ```

4. **Acceder a la aplicación**:
   - Visita: http://localhost:3000

## 🎓 Recuerda

- **Antes de cada tarea**: Llama a `context-engineer` para cargar contexto
- **Para nuevas características**: Usa `feature-flow-manager`
- **Para decisiones de producto**: Usa `product-owner`
- **Para UI/estilos**: Usa `tailwind-specialist`
- **Para arquitectura**: Usa `rails-architect`
- **Para interactividad**: Usa `hotwire-specialist`

¡Todos los agentes están alineados y listos para ayudarte con la implementación! 🎉
```

## Criterios de Éxito

- ✅ Aplicación Rails creada en carpeta actual
- ✅ CLAUDE.md inicializado con instrucciones de agentes
- ✅ Característica v1.0-mvp creada en Feature Flow Manager
- ✅ Product Owner ha definido MVP con JTBD y PRD
- ✅ Los 3 agentes técnicos han completado sus planes
- ✅ Código implementado según planes de agentes
- ✅ Context Engineer ha documentado todas las decisiones
- ✅ Usuario puede ejecutar `bin/dev` y ver la app funcionando
- ✅ Todos los artefactos están guardados y organizados

## Gestión de Errores

- Si algún agente falla, reporta qué fase falló y por qué
- Permite al usuario reintentar fases individuales
- Proporciona resultados parciales si algunos agentes tienen éxito
- Sugiere completar manualmente las fases que fallaron

## Notas Importantes

- La aplicación se crea en la **carpeta actual**, no en un subdirectorio
- Los agentes técnicos (paso 5) se ejecutan **en paralelo** para eficiencia
- El Product Owner define **lo mínimo** para validar la idea, no todas las características posibles
- Context Engineer documenta **al final** para capturar todas las decisiones tomadas
- CLAUDE.md instruye a **siempre** usar context-engineer antes de cualquier tarea
