---
description: Initialize design system for the project
allowed-tools: ["Task", "Read", "Write", "Edit", "Glob", "Grep"]
---

# Inicializar Sistema de Diseño

Este comando inicializa el sistema de diseño del proyecto creando la estructura de directorio y documentación base para mantener consistencia visual en toda la aplicación.

**Uso**: `/system-design:init`

## Descripción

El comando delega al agente especializado `design-system-manager` la responsabilidad de:

1. Crear la estructura de directorios para el sistema de diseño
2. Establecer guías visuales base (colores, tipografía, espaciado)
3. Documentar componentes de UI estándar
4. Configurar tokens de diseño para Tailwind CSS
5. Generar documentación inicial del sistema

## Implementación

Usa el agente `design-system-manager` para inicializar un sistema de diseño completo:

**IMPORTANTE**: Delega TODA la responsabilidad al agente especializado. No implementes nada directamente.

### Instrucciones para el Agente

Lanza el agente `design-system-manager` con la siguiente tarea:

```
Inicializa el sistema de diseño para este proyecto. Necesito que:

1. Crees la estructura de directorio `.contexts/design-system/` si no existe
2. Generes el archivo `visual-guidelines.md` con:
   - Paleta de colores definida y justificada
   - Sistema tipográfico (fuentes, escalas, pesos)
   - Sistema de espaciado (padding, margin, gaps)
   - Sistema de componentes base (botones, inputs, cards, modales, etc.)
   - Especificaciones de diseño responsive

3. Identifiques el framework CSS del proyecto (Tailwind, Bootstrap, CSS-in-JS, etc.)
4. Si el proyecto usa Tailwind CSS, actualices la configuración con los tokens del sistema de diseño
5. Documentes las decisiones tomadas y las razones detrás de ellas

Si no tienes suficiente información sobre la personalidad o marca del proyecto, hazme preguntas específicas antes de generar el sistema de diseño.

El sistema debe ser práctico, implementable inmediatamente, y servir como fuente única de verdad para todas las decisiones visuales del proyecto.
```

### Flujo de Ejecución

1. **Análisis del proyecto**: El agente inspeccionará el proyecto para entender:
   - Framework de CSS usado (Tailwind, Bootstrap, etc.)
   - Tipo de aplicación (web, móvil, dashboard, etc.)
   - Stack tecnológico

2. **Recopilación de información**: Si es necesario, el agente preguntará sobre:
   - Personalidad de marca (formal, casual, técnica, creativa)
   - Audiencia objetivo
   - Casos de uso principales
   - Referencias visuales o inspiración

3. **Generación del sistema**: El agente creará:
   - Documentación completa en `.contexts/design-system/visual-guidelines.md`
   - Configuración de tokens (si aplica)
   - Especificaciones de componentes listos para implementar

4. **Validación**: El agente presentará el sistema generado y solicitará feedback

## Resultado Esperado

Después de ejecutar este comando, tendrás:

- ✅ Estructura de directorio `.contexts/design-system/` creada
- ✅ Archivo `visual-guidelines.md` con sistema de diseño completo
- ✅ Tokens de diseño configurados (si usa Tailwind CSS)
- ✅ Especificaciones de componentes documentadas
- ✅ Guías de uso y mejores prácticas
- ✅ Sistema versionado y listo para evolucionar

## Ejemplos de Uso

### Inicialización básica
```bash
/system-design:init
```

### Después de la inicialización

El sistema de diseño estará disponible en:
- `.contexts/design-system/visual-guidelines.md` - Documentación principal
- `tailwind.config.js` - Tokens configurados (si aplica)

Otros comandos podrán consultar este sistema para:
- Obtener clases CSS exactas para componentes
- Verificar consistencia visual
- Generar nuevos componentes siguiendo el sistema

## Notas

- Este comando es idempotente: si el sistema ya existe, el agente lo actualizará en lugar de recrearlo
- El agente solicitará confirmación antes de sobrescribir archivos existentes
- El sistema generado es la base para todos los componentes visuales del proyecto
- Otros agentes especializados (como `tailwind-specialist`) consultarán este sistema

## Comandos Relacionados

- `/design-system:update` - Actualizar el sistema de diseño existente
- `/design-system:audit` - Auditar consistencia del diseño en el código
- `/design-system:component` - Registrar nuevo componente en el sistema
