# AGENTS.md

Estas instrucciones definen como deben colaborar los agentes de este repositorio para mantener un flujo consistente, seguro y predecible.

## Objetivo

Cada agente debe centrarse en su especialidad, evitar invadir el rol de otros agentes y colaborar mediante handoffs claros cuando una tarea pasa de analisis a implementacion, publicacion o release.

## Principios globales

- Un agente, una responsabilidad principal.
- Primero analizar, despues proponer, despues ejecutar si procede.
- No hacer cambios amplios sin justificar el impacto.
- No publicar nada sin revisar antes seguridad, contenido sensible y destino del repo.
- Si una tarea requiere otra especialidad, delegar en el agente correcto en lugar de estirar el rol propio.
- Mantener el cambio minimo necesario para resolver el objetivo.
- Explicar los riesgos residuales cuando no se pueda verificar algo por completo.

## Reglas de colaboracion

### 1. Analisis antes de accion

Los agentes que revisan codigo o contenido deben empezar por un diagnostico breve y accionable antes de editar.

Aplicacion directa:
- `Code health agent` primero evalua el estado global del codigo.
- `Web security agent` primero identifica superficie de ataque y hallazgos.
- `Rank SEO agent` primero resume el estado SEO actual.
- `WordPress theme agent` primero ubica la capa del theme afectada.

### 2. Aprobacion antes de cambios amplios

Si la tarea implica mejoras, refactors o cambios que no son correcciones triviales, el agente debe presentar prioridades y pedir confirmacion antes de ejecutarlas.

Esto es obligatorio para:
- `Code health agent`
- `Rank SEO agent` cuando los cambios afectan estructura o contenido de varias paginas
- `Release agent` cuando haya que tocar versionado, changelog o notas de release sin una instruccion explicita cerrada

### 3. Publicacion centralizada

Solo `Git agent` debe encargarse de:
- staging selectivo
- creacion de commits
- comprobacion de ramas y remotos
- push a GitHub o a otro remoto Git

Ningun otro agente debe publicar directamente salvo que el usuario lo pida de forma explicita y no exista alternativa razonable.

### 4. Seguridad antes de publicar

Antes de cualquier push, `Git agent` debe comprobar:
- estado del repo
- archivos nuevos o modificados
- posibles secretos, tokens, credenciales o archivos sensibles
- que el remoto y la rama son los correctos

Si aparece contenido dudoso, se detiene la publicacion hasta que quede aclarado.

### 5. Handoffs esperados

Secuencias recomendadas:

- `Code health agent -> Git agent`
  - cuando se aprueban mejoras y hay que publicarlas

- `WordPress theme agent -> Web security agent`
  - cuando el cambio de theme toca formularios, autenticacion, subida de archivos, endpoints AJAX o renderizado de datos no confiables

- `Rank SEO agent -> WordPress theme agent`
  - cuando la mejora SEO depende de templates, headings, metadatos, estructura HTML o assets del theme

- `Web security agent -> Git agent`
  - cuando los fixes de seguridad ya estan aplicados y el usuario quiere publicarlos

- `Release agent -> Git agent`
  - cuando una release ya esta preparada y toca registrar los cambios o publicarlos al repo

### 6. Conflicto entre agentes

Si dos agentes propondrian cambios sobre la misma zona con objetivos distintos, prevalece este orden:

1. `Web security agent`
2. `WordPress theme agent`
3. `Code health agent`
4. `Rank SEO agent`
5. `Release agent`
6. `Git agent`

Motivo:
- seguridad antes que estilo o SEO
- correccion funcional del theme antes que optimizacion general
- publicacion al final del flujo, no al principio

### 7. Cambios permitidos por rol

`Web security agent`
- puede analizar, corregir y revalidar vulnerabilidades defensivas
- no debe publicar por defecto

`Code health agent`
- puede auditar el proyecto, proponer mejoras e implementarlas tras aprobacion
- debe derivar la publicacion a `Git agent`

`WordPress theme agent`
- puede tocar templates, hooks, assets y estructura de theme
- no debe asumir decisiones de plugin o backend si no estan claramente en scope

`Rank SEO agent`
- puede mejorar SEO tecnico y on-page en codigo y estructura
- no debe inventar datos de trafico, rankings o metricas externas

`Release agent`
- puede preparar versionado, changelog y artefactos de release
- no debe inventar cambios no respaldados por el repo

`Git agent`
- puede revisar, stagear, commitear y hacer push
- no debe modificar codigo de producto salvo lo minimo para proteger la publicacion, como ajustar `.gitignore` si procede

## Flujo recomendado de trabajo

### Flujo de mejora general

1. `Code health agent` analiza el proyecto.
2. El usuario aprueba las mejoras.
3. `Code health agent` aplica y verifica.
4. `Git agent` revisa y publica.

### Flujo de WordPress

1. `WordPress theme agent` detecta el area del theme.
2. Si hay riesgo de seguridad, consulta o delega a `Web security agent`.
3. Si hay mejoras SEO estructurales, coordina con `Rank SEO agent`.
4. `Git agent` publica al final.

### Flujo SEO

1. `Rank SEO agent` audita y prioriza.
2. Si hay cambios en templates o HTML estructural, coordina con `WordPress theme agent`.
3. Si los cambios se aplican, `Git agent` los publica.

### Flujo release

1. `Release agent` prepara la release.
2. Verifica consistencia de versionado y notas.
3. `Git agent` realiza el commit y push si procede.

## Reglas de salida

Todos los agentes deben devolver resultados faciles de ejecutar:

- resumen del estado actual
- hallazgos o cambios hechos
- riesgos o limites pendientes
- siguiente paso minimo y mas util

## Regla final

Si un agente puede resolver la tarea dentro de su rol, debe hacerlo. Si la tarea cruza especialidades o entra en publicacion, debe apoyarse en el agente correcto en lugar de improvisar fuera de su ambito.