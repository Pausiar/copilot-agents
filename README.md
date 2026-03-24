# Copilot Agents

Coleccion de agentes personalizados para GitHub Copilot en VS Code.

Este repositorio agrupa agentes orientados a tareas concretas para trabajar con mas consistencia, menos contexto irrelevante y mejores flujos de trabajo.

## Agentes incluidos

### Web security agent
Revisa una web o aplicacion web en busca de vulnerabilidades comunes y especificas del proyecto, aplica fixes defensivos y vuelve a validar el resultado.

Casos de uso:
- Auditoria de seguridad web
- Reforzar proyectos WordPress o PHP
- Corregir XSS, CSRF, inyecciones y problemas de manejo de archivos

### Git agent
Prepara commits y pushes de forma segura, revisando el estado del repo y evitando la publicacion accidental de secretos o archivos sensibles.

Casos de uso:
- Subir cambios a GitHub
- Revisar staging antes de publicar
- Confirmar ramas, remotos y contenido sensible

### Code health agent
Analiza el codigo de forma global para valorar interconexion, funcionalidad, mantenibilidad y optimizacion. Primero entrega un diagnostico y despues puede aplicar mejoras aprobadas. Si hay cambios, puede apoyarse en Git agent para publicarlos.

Casos de uso:
- Revisiones generales del proyecto
- Detectar puntos debiles de arquitectura o mantenimiento
- Aplicar mejoras tras aprobacion

### Release agent
Prepara una release revisando versionado, changelog, notas de version y consistencia entre archivos relacionados.

Casos de uso:
- Preparar una nueva version
- Validar checklist de release
- Revisar si falta metadata antes de publicar

### WordPress theme agent
Especializado en temas WordPress: templates, hooks, jerarquia de plantillas, assets, compatibilidad y mantenimiento de la capa de theme.

Casos de uso:
- Corregir templates de WordPress
- Revisar hooks y estructura del tema
- Implementar mejoras de theme sin mezclar responsabilidades de plugin

### Rank SEO agent
Audita y mejora el SEO tecnico y on-page de una web: estructura, metadatos, headings, enlazado interno, oportunidades de schema y senales generales de indexacion y visibilidad.

Casos de uso:
- Mejorar SEO tecnico
- Revisar paginas prioritarias
- Corregir estructuras que afectan al posicionamiento

## Estructura

Los agentes estan guardados en:

```text
.github/agents/
```

Cada archivo `.agent.md` define:
- descripcion del agente
- herramientas permitidas
- instrucciones de comportamiento
- formato de salida esperado

## Uso en VS Code

1. Abre el selector de agentes en GitHub Copilot Chat.
2. Elige el agente que mejor encaje con la tarea.
3. Describe el contexto del proyecto y el objetivo.

Ejemplos de prompts:

```text
Use Web security agent para revisar este tema WordPress y corregir vulnerabilidades.
```

```text
Use Git agent para preparar commit y push de los cambios, excluyendo archivos sensibles.
```

```text
Use Code health agent para evaluar la calidad general del proyecto y proponer mejoras.
```

```text
Use Rank SEO agent para revisar esta web y aplicar mejoras SEO tecnicas prioritarias.
```

## Objetivo del repositorio

Mantener una base reutilizable de agentes especializados para acelerar tareas frecuentes con un comportamiento mas predecible y orientado a resultados.