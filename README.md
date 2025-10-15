# Configuración Software 3.0 para Claude Code

Un repositorio de configuración **Software 3.0** que extiende Claude Code con flujos de trabajo de desarrollo potentes, agentes especializados y comandos simplificados diseñados tanto para desarrolladores como para no desarrolladores.

## Qué es esto

Este repositorio proporciona un entorno de desarrollo completo para Claude Code con cuatro sistemas principales:

1. **Comandos VCS** - Operaciones de control de versiones simplificadas en lenguaje natural
2. **Gestión de Features** - Ciclo de vida completo del desarrollo de producto desde la idea hasta la implementación
3. **Agentes Especializados** - Agentes de IA expertos en Rails, Hotwire, Tailwind, Gestión de Producto y Sistemas de Diseño
4. **Sistema de Aprendizaje** - Actualización automática de documentación mediante análisis de conversaciones

## Características

### VCS (Sistema de Control de Versiones)
✨ **Comandos en Lenguaje Natural** - No se requiere jerga técnica
🤖 **Mensajes de Commit Autogenerados** - Análisis inteligente de tus cambios
🎯 **Operaciones Selectivas de Archivos** - Guarda archivos específicos usando descripciones naturales
🔄 **Historial Interactivo** - Navega y elige versiones visualmente
📊 **Análisis Inteligente de Cambios** - Comprende el impacto de tus modificaciones
🏷️ **Etiquetado Fácil de Versiones** - Marca hitos importantes sin esfuerzo
🧹 **Operaciones de Limpieza Seguras** - Descarta cambios no deseados con confirmación

### Gestión de Features
🎯 **Jobs To Be Done (JTBD)** - Define problemas del cliente antes de construir soluciones
📋 **Product Requirements (PRD)** - Crea especificaciones completas de features
📐 **Planificación Técnica** - Organiza la implementación con decisiones arquitectónicas
🔄 **Gestión del Ciclo de Vida** - Rastrea features desde la creación hasta el archivo
💾 **Persistencia de Estado** - Mantén el contexto de features entre sesiones
🗂️ **Organización de Features** - Lista, cambia, archiva y restaura features

### Agentes de IA Especializados
🏗️ **Rails Architect** - Principios SOLID, patrones de arquitectura y mejores prácticas
⚡ **Hotwire Specialist** - Turbo Frames, Turbo Streams y controladores Stimulus
🎨 **Tailwind Specialist** - CSS utility-first, diseño responsive y optimización
📊 **Product Owner** - Gestión de producto lean y priorización

### Sistema de Aprendizaje
🧠 **Análisis de Conversaciones** - Extrae insights de sesiones de desarrollo
📚 **Auto-Documentación** - Actualiza CLAUDE.md con patrones aprendidos
🔄 **Aprendizaje Continuo** - Mantén la documentación sincronizada con la evolución del proyecto
🎯 **Actualizaciones Selectivas** - Apunta a secciones específicas para documentación focalizada
📊 **Reconocimiento de Patrones** - Identifica decisiones arquitectónicas y mejores prácticas

## Inicio Rápido

### Sistema de Control de Versiones (VCS)

#### 1. Inicializar Control de Versiones
```bash
/vcs:iniciar
```
Comienza a rastrear cambios en tu proyecto.

#### 2. Guardar tu Trabajo
```bash
# Guardar todos los cambios con mensaje autogenerado
/vcs:guardar

# Guardar con mensaje personalizado
/vcs:guardar -m "Añadido sistema de autenticación"

# Guardar archivos específicos usando lenguaje natural
/vcs:guardar "todos los archivos JavaScript" -m "Corregidos bugs de login"
/vcs:guardar "archivos en carpeta src"
/vcs:guardar "archivos de configuración"
```

#### 3. Comprobar tu Progreso
```bash
# Ver qué has cambiado
/vcs:diferencias

# Ver tu historial de guardados
/vcs:historial

# Ver los últimos 5 guardados
/vcs:historial 5
```

#### 4. Volver a Versiones Anteriores
```bash
# Mostrar historial y elegir interactivamente
/vcs:cargar

# Cargar versión específica por hash
/vcs:cargar abc123f

# Cargar versión etiquetada
/vcs:cargar version-1-0

# Volver un guardado atrás
/vcs:cargar HEAD~1
```

#### 5. Marcar Hitos Importantes
```bash
# Crear etiqueta con timestamp
/vcs:etiquetar

# Crear etiqueta con nombre
/vcs:etiquetar "versión 1.0"
/vcs:etiquetar "release estable"
```

#### 6. Limpiar Cambios No Deseados
```bash
# Descartar todos los cambios sin confirmar
/vcs:limpiar

# Limpiar solo archivos específicos
/vcs:limpiar src/auth.js README.md
/vcs:limpiar "*.js"
```

### Flujo de Trabajo de Gestión de Features

#### 1. Crear una Nueva Feature
```bash
# Iniciar una nueva feature con flujo guiado
/feature:crear

# El sistema te guiará a través de:
# - Nombre y descripción de la feature
# - Creación del documento JTBD (Jobs To Be Done)
# - Creación del documento PRD (Product Requirements Document)
# - Creación del plan técnico de implementación
```

#### 2. Trabajar en Features
```bash
# Cambiar entre features
/feature:cambiar nombre-feature

# Comprobar estado de la feature actual
/feature:estado

# Listar todas las features
/feature:listar

# Programar código desde el plan (siguiente tarea o todas)
/feature:programar siguiente
/feature:programar todo
```

#### 3. Organizar y Planificar
```bash
# Crear documentos de planificación independientes
/feature:crear-jtbd    # Análisis Jobs To Be Done
/feature:crear-prd     # Product Requirements Document
/feature:crear-plan    # Plan técnico de implementación
/feature:organizar-plan  # Organizar plan existente
```

#### 4. Ciclo de Vida de Features
```bash
# Archivar features completadas
/feature:archivar nombre-feature

# Mover a papelera (eliminación suave)
/feature:papelera nombre-feature

# Restaurar desde papelera
/feature:restaurar nombre-feature
```

### Aprendizaje y Documentación

```bash
# Analizar conversación y actualizar CLAUDE.md
/aprender

# Actualizar solo una sección específica
/aprender arquitectura
/aprender principios
```

El comando `/aprender` analiza tu conversación actual para extraer:
- Decisiones técnicas tomadas
- Nuevos patrones descubiertos
- Cambios de arquitectura
- Mejores prácticas aprendidas
- Adiciones de features

Luego actualiza automáticamente el archivo CLAUDE.md para mantener la documentación sincronizada con la evolución del proyecto.

### Usar Agentes Especializados

Los agentes especializados están disponibles automáticamente y pueden invocarse directamente en tus conversaciones:

```
"Necesito implementar autenticación de usuario en Rails"
→ El agente Rails Architect proporciona guía de arquitectura SOLID

"¿Cómo añado edición inline con Hotwire?"
→ El Hotwire Specialist proporciona implementación con Turbo Frame

"Estiliza este formulario con Tailwind"
→ El Tailwind Specialist proporciona implementación CSS utility-first

"¿Deberíamos construir esta feature?"
→ El Product Owner ayuda con análisis JTBD y priorización
```

## Comandos Disponibles

### Comandos VCS

| Comando | Descripción |
|---------|-------------|
| `/vcs:iniciar` | Inicializar control de versiones en el directorio actual |
| `/vcs:guardar [archivos] [-m "mensaje"]` | Guardar cambios con mensajes de commit inteligentes |
| `/vcs:cargar [commit]` | Restaurar a versión anterior |
| `/vcs:historial [cantidad]` | Ver historial de guardados |
| `/vcs:diferencias` | Mostrar cambios pendientes con análisis |
| `/vcs:etiquetar [mensaje]` | Crear etiquetas de versión |
| `/vcs:limpiar [archivos]` | Descartar cambios de forma segura |
| `/vcs:ayuda` | Mostrar ayuda detallada |

### Comandos de Gestión de Features

| Comando | Descripción |
|---------|-------------|
| `/feature:crear` | Crear nueva feature con flujo guiado |
| `/feature:cambiar [nombre]` | Cambiar a una feature diferente |
| `/feature:estado` | Mostrar estado de la feature actual |
| `/feature:listar` | Listar todas las features (activas/archivadas/papelera) |
| `/feature:archivar [nombre]` | Archivar feature completada |
| `/feature:papelera [nombre]` | Mover feature a papelera |
| `/feature:restaurar [nombre]` | Restaurar feature desde papelera |
| `/feature:crear-jtbd` | Crear documento Jobs To Be Done |
| `/feature:crear-prd` | Crear Product Requirements Document |
| `/feature:crear-plan` | Crear plan técnico de implementación |
| `/feature:organizar-plan` | Organizar plan existente |
| `/feature:programar [siguiente\|todo]` | Programar tareas del plan (siguiente o todas) |

### Comandos de Utilidad

| Comando | Descripción |
|---------|-------------|
| `/gestor-comandos` | Gestionar comandos slash (crear, editar, eliminar) |
| `/aprender [sección]` | Analizar conversación y actualizar CLAUDE.md con insights |

## Selección de Archivos en Lenguaje Natural

Los comandos `vcs:guardar` y `vcs:limpiar` entienden descripciones naturales:

- **Tipos de archivo**: `"archivos JavaScript"`, `"scripts Python"`, `"archivos de configuración"`
- **Carpetas**: `"archivos en carpeta src"`, `"todo en directorio docs"`
- **Patrones**: `"archivos de test"`, `"documentación"`, `"scripts de build"`
- **Archivos específicos**: `"package.json yarn.lock"`, `"README.md src/main.js"`

## Características Inteligentes

### Mensajes de Commit Autogenerados
Cuando usas `/vcs:guardar` sin mensaje, el sistema analiza tus cambios y crea mensajes de commit profesionales como:
- `feat: añadir sistema de autenticación de usuario`
- `fix: resolver problema de conexión a base de datos`
- `docs: actualizar guía de instalación`
- `config: configurar entorno de desarrollo`

### Análisis Inteligente de Cambios
El comando `/vcs:diferencias` proporciona:
- **Resumen de Impacto del Proyecto** - Qué significan tus cambios
- **Resumen de Trabajo** - Tipo de trabajo realizado
- **Análisis de Archivos** - Explicación detallada de cada cambio
- **Evaluación de Preparación** - Si los cambios están listos para guardar

### Historial Interactivo
Usar `/vcs:cargar` sin parámetros muestra tu historial de commits y te permite elegir qué versión restaurar interactivamente.

## Características de Seguridad

- **Confirmaciones Explícitas** - Las operaciones destructivas requieren escribir "sí"
- **Vistas Previas Detalladas** - Ve exactamente qué cambiará antes de proceder
- **Análisis de Impacto** - Comprende qué perderás antes de limpiar/cargar
- **Operaciones Selectivas** - Apunta a archivos específicos sin afectar otros

## Instalación

1. **Carga esta configuración en Claude Code**:
   - Abre tu proyecto en Claude Code
   - Asegúrate de que este repositorio de configuración sea accesible
   - Los comandos VCS estarán disponibles como comandos slash

2. **Comienza a usar los comandos VCS**:
   ```bash
   /vcs:iniciar    # Inicializa tu proyecto
   /vcs:ayuda      # Ver todos los comandos disponibles
   ```

## Flujo de Trabajo de Ejemplo

```bash
# Iniciar un nuevo proyecto
/vcs:iniciar

# Trabaja en tus archivos...
# Añade features, corrige bugs, actualiza docs

# Comprueba qué has hecho
/vcs:diferencias

# Guarda tu trabajo
/vcs:guardar "Añadida autenticación y mejorados docs"

# Continúa trabajando...

# Guarda solo cambios específicos
/vcs:guardar "archivos de test" -m "Añadidos tests unitarios"

# Marca un hito
/vcs:etiquetar "beta release"

# Ve tu progreso
/vcs:historial

# ¿Necesitas volver atrás?
/vcs:cargar

# Limpia cambios experimentales
/vcs:limpiar "experimental-feature.js"
```

## Agentes de IA Especializados

Esta configuración incluye cuatro agentes de IA expertos con conocimiento profundo del dominio:

### 🏗️ Rails Architect
**Experiencia**: Arquitectura Rails, principios SOLID, patrones de diseño
- Toma de decisiones arquitectónicas (Service Objects, STI vs polimorfismo)
- Revisión de código contra principios SOLID/KISS/YAGNI
- Estrategias de refactorización y patrones de migración
- Diseño conforme a REST
- **Líneas de código**: 55.278 líneas de experiencia estructurada

### ⚡ Hotwire Specialist
**Experiencia**: Turbo Drive, Turbo Frames, Turbo Streams, Stimulus
- Decidir qué técnica Hotwire para features específicas
- Implementar edición inline, modales, actualizaciones en tiempo real
- Depurar desajustes de Turbo Frame
- Configuración de broadcast ActionCable
- **Líneas de código**: 35.940 líneas de patrones Hotwire

### 🎨 Tailwind Specialist
**Experiencia**: CSS utility-first, diseño responsive, rendimiento
- Implementar componentes UI con utilidades Tailwind
- Configuración y personalización de tema
- Optimización de tamaño de bundle y PurgeCSS
- Implementación de modo oscuro
- Accesibilidad con Tailwind
- **Líneas de código**: 38.519 líneas de experiencia CSS

### 📊 Product Owner (Lean)
**Experiencia**: Jobs To Be Done, priorización de producto, metodología lean
- Descubrimiento JTBD antes de construir features
- Crear Product Requirements Documents
- Frameworks de priorización (RICE, Kano)
- Gestión de alcance y decir "no"
- Análisis de métricas post-lanzamiento
- **Líneas de código**: 46.326 líneas de conocimiento de producto

**Conocimiento Total de Agentes**: Más de 176.000 líneas de conocimiento experto estructurado

## Perfecto Para

### Usuarios No Técnicos
- **Creadores de contenido** rastreando versiones de documentos
- **Diseñadores** versionando assets creativos
- **Gestores de proyecto** organizando desarrollo de features
- **Cualquiera** que quiera control de versiones simple

### Desarrolladores
- **Desarrolladores Rails** construyendo aplicaciones mantenibles
- **Desarrolladores full-stack** usando Hotwire y Tailwind
- **Desarrolladores solitarios** necesitando guía arquitectónica
- **Equipos** queriendo patrones de diseño consistentes

### Equipos de Producto
- **Gestores de producto** definiendo features con JTBD
- **Diseñadores** manteniendo sistemas de diseño
- **Stakeholders** entendiendo el ciclo de vida del desarrollo

## Detalles Técnicos

### Arquitectura

Esta configuración extiende Claude Code a través de tres componentes principales:

#### 1. Comandos Slash
Comandos personalizados definidos como archivos markdown en `.claude/commands/`:
- **Comandos VCS** (`vcs/`) - 8 comandos para control de versiones
- **Comandos Feature** (`feature/`) - 12 comandos para gestión del ciclo de vida de features
- **Comandos de Utilidad** - Gestor de comandos y sistema de aprendizaje para auto-mejora

#### 2. Agentes Especializados
Agentes de IA con experiencia de dominio en `.claude/agents/`:
- Cada agente contiene más de 30.000 líneas de conocimiento estructurado
- Usa framework de 6 contextos (c₁-c₆) para respuestas consistentes
- Invocados automáticamente según el contexto de la conversación
- Proporciona guía experta en dominios específicos

#### 3. Gestión de Estado
Rastreo de estado persistente para features:
- `_features/active/` - Desarrollo de features activas
- `_features/archived/` - Features completadas
- `_features/trashed/` - Features eliminadas suavemente
- `_features/state.json` - Feature actual y metadatos

### Estructura de Archivos
```
.claude/
├── commands/
│   ├── vcs/           # 8 comandos VCS
│   ├── feature/       # 12 comandos de gestión de features
│   ├── gestor-comandos.md
│   └── aprender.md    # Comando del sistema de aprendizaje
├── agents/
│   ├── rails-architect.md        # 55.278 líneas
│   ├── hotwire-specialist.md     # 35.940 líneas
│   ├── tailwind-specialist.md    # 38.519 líneas
│   └── product-owner.md          # 46.326 líneas
└── settings.local.json

_features/
├── active/           # Features activas
├── archived/         # Features archivadas
├── trashed/          # Features eliminadas suavemente
└── state.json        # Estado de feature actual
```

**Sin comandos tradicionales de build/test** - Este es un repositorio de configuración que extiende las capacidades de Claude Code.

## Innovaciones Clave

### 1. Desarrollo Dirigido por Producto
En lugar de solo escribir código, empieza con problemas del cliente:
- **JTBD Primero**: Entiende el trabajo que los clientes están tratando de hacer
- **Documentación PRD**: Define requisitos antes de la implementación
- **Planificación Técnica**: Organiza la arquitectura antes de codificar
- **Rastreo del Ciclo de Vida**: Gestiona features desde la idea hasta el archivo

### 2. Colaboración con IA Experta
Cuatro agentes especializados proporcionan experiencia profunda del dominio:
- **176.000+ líneas** de conocimiento estructurado
- **Framework de 6 contextos** asegura respuestas consistentes de alta calidad
- **Invocación automática** según el contexto de la conversación
- **Experiencia complementaria** a través de producto e ingeniería

### 3. Flujos de Trabajo Simplificados
Operaciones complejas hechas simples:
- **Lenguaje natural** en lugar de comandos técnicos
- **Flujos guiados** para creación de features
- **Artefactos autogenerados** (mensajes de commit, PRDs, planes)
- **Confirmaciones de seguridad** para operaciones destructivas

### 4. Sistema Auto-Documentado
Una configuración de aprendizaje que se mejora a sí misma:
- **Análisis de conversaciones** extrae patrones y decisiones automáticamente
- **Actualizaciones de CLAUDE.md** mantienen la documentación sincronizada con la realidad
- **Aprendizaje continuo** de cada sesión de desarrollo
- **Reconocimiento de patrones** identifica mejores prácticas arquitectónicas
- **Acumulación de conocimiento** construye mejor contexto para trabajo futuro

## Soporte

### Obtener Ayuda
- Usa `/vcs:ayuda` para documentación de comandos VCS
- Usa `/feature:listar` para ver todos los comandos de gestión de features
- Consulta `.claude/commands/` para especificaciones detalladas de comandos
- Los agentes proporcionan guía automáticamente en sus dominios

### Descubrimiento de Comandos
- Escribe `/` en Claude Code para ver todos los comandos disponibles
- Usa `/gestor-comandos` para crear comandos personalizados
- Explora el directorio `.claude/commands/` para ejemplos

---

**Software 3.0** - Donde la IA entiende tu intención, proporciona guía experta y maneja la complejidad técnica mientras tú te enfocas en construir grandes productos.
