---
id: "20260719030000"
tipo: convenciones
estado: vigente
tags: [configuracion, convenciones, fundacional]
relacionado_con: ["[[Arquitectura Cognitiva del Sistema]]", "[[Epistemología del Sistema]]", "[[Manifiesto del Proyecto - SACP]]"]
padre: "[[Índice]]"
aliases: [Convenciones, Convenciones del vault]
---

# Convenciones del vault

Este documento reúne las reglas prácticas de organización del vault: cómo se nombran los archivos, cómo se estructura el frontmatter, qué va en cada nivel de conocimiento, y qué información puede o no vivir en la memoria permanente. Es el complemento operativo de [[Arquitectura Cognitiva del Sistema]] y [[Epistemología del Sistema]], que explican el porqué; este documento explica el cómo.

## 1. Organización de carpetas

El vault combina dos criterios: **carpetas por tipo** (`Conceptos/`, `Proyectos/`, `Decisiones/`, etc.) para navegación básica, y **frontmatter relacional** (`relacionado_con`, `padre`, `sintetiza`, `evidencia_base`) para la relación real entre notas. Las carpetas organizan; los enlaces y el frontmatter conectan. Ante una colisión conceptual entre una carpeta nueva y contenido que ya vive en otra carpeta, la solución nunca es duplicar contenido: se crea una única nota de síntesis que enlaza (ver §5).

## 2. Estructura de tres niveles de conocimiento

- **Nivel 1 — Conocimiento atómico**: `Conceptos/`, `Investigaciones/`, `Descubrimientos/`, `Patrones/`, `Hipótesis/`, `Fuentes/`, `Decisiones/`, más la capa operacional `Proyectos/`, `Personas/`, `Conversaciones/`.
- **Nivel 2 — Modelos**: la carpeta `Modelos/` sintetiza varias piezas de Nivel 1 en explicaciones de dominio con poder explicativo y predictivo.
- **Nivel 3 — Modelo del Mundo**: emergente, sin carpeta ni nota propia. Es la comprensión acumulada de todo el grafo de conocimiento conectado.

Ver [[Arquitectura Cognitiva del Sistema]] §3 para el detalle completo, y [[Epistemología del Sistema]] §3 para la escalera dato → concepto → patrón → hipótesis → modelo que rige cómo una pieza de conocimiento asciende de nivel.

## 3. Idioma y nomenclatura

- Todo el contenido del vault se escribe en español, incluyendo nombres de carpeta y archivo (con tildes y eñes cuando corresponda).
- Los nombres de archivo son descriptivos, no códigos ni abreviaturas (ej. `Manifiesto del Proyecto - SACP.md`, no `manifiesto-sacp.md`).
- Cada nota lleva un campo `id` en frontmatter con formato `"YYYYMMDDHHmmss"` (string), el timestamp real de creación. Esto da estabilidad a los enlaces incluso si el título del archivo cambia con el tiempo. Si varias notas se crean en el mismo lote/segundo, se incrementa el último dígito para mantener unicidad.
- Los nombres de archivo pueden cambiar libremente sin romper la identidad de la nota, porque la identidad real la da `id`, no el nombre.

## 4. Criterio de admisión a la memoria

Antes de crear cualquier nota de contenido curado (Nivel 1, Nivel 2, o Modelo del Usuario), se aplica esta pregunta:

**Pregunta central: ¿Esta información aumentará la capacidad futura del sistema para comprender, razonar o tomar mejores decisiones?**

Guía no obligatoria (basta justificar afirmativamente 1-2, no todas):
- ¿Ayuda a construir o mejorar un modelo?
- ¿Conecta conocimientos previamente separados?
- ¿Permite detectar un patrón?
- ¿Será útil para futuras investigaciones?
- ¿Aporta contexto para decisiones futuras?
- ¿Representa un aprendizaje difícil de reconstruir posteriormente?
- ¿Es suficientemente estable como para formar parte del conocimiento de largo plazo?

El objetivo no es almacenar mucho, sino aumentar progresivamente la inteligencia del sistema. Este criterio vive en tres lugares del vault, deliberadamente: la adenda de [[Manifiesto del Proyecto - SACP]], este documento, y el footer "¿Por qué vive esto en la memoria permanente?" presente en cada plantilla de nota de contenido curado en `Sistema/Plantillas/`.

## 5. Bitácora vs. memoria permanente

`Sistema/Bitácora/` es zona de captura cruda, no memoria curada. Las notas diarias (`Plantilla - Bitácora diaria.md`) no llevan el footer de admisión a la memoria porque no son, por sí mismas, conocimiento permanente — son el lugar donde algo puede empezar antes de decidir si merece vivir en la memoria. Lo que en una entrada de bitácora resulte valioso se **promueve** explícitamente a una nota de Nivel 1 (Concepto, Patrón, Descubrimiento, etc.); en ese momento, y solo en ese momento, pasa por el criterio de admisión del §4.

## 6. Regla general de no-duplicación

Cuando dos carpetas del vault podrían razonablemente contener la misma información (por ejemplo, `Modelo del Usuario/Proyectos Activos/` frente a `/Proyectos/`, o `Modelo del Usuario/Historial de Decisiones/` frente a `/Decisiones/`), la regla es: **el contenido vive en un solo lugar, y el otro lugar contiene únicamente una nota de síntesis que enlaza**. Esa nota de síntesis (`Plantilla - Síntesis (Modelo del Usuario).md`) incluye un bloque de consulta inerte (formato `FROM "<Carpeta>" WHERE <condición>`) que se activará automáticamente cuando se instale el plugin Dataview. Esta regla se generaliza a cualquier colisión futura similar entre carpetas del vault: nunca copiar contenido, siempre enlazar y, si aplica, sintetizar.

## 7. Plugins preparados pero no instalados

El vault se preparó para tres plugins de comunidad que el usuario puede instalar manualmente cuando lo decida. Ninguno se activó en `.obsidian/community-plugins.json` (ese archivo no existe todavía en el vault) porque instalarlo sin los binarios físicos del plugin no tiene efecto y puede mostrar avisos de "plugin roto" en Obsidian.

- **Dataview** — las plantillas y MOCs que se benefician de consultas dinámicas (ej. `Síntesis.md` en Modelo del Usuario, o los MOCs de tipo) contienen bloques de consulta inertes (formato texto plano, no bloques ```dataview reales) listos para activarse.
- **Templater** — las plantillas en `Sistema/Plantillas/` usan sintaxis `<% tp.date.now(...) %>` y `<% tp.file.title %>`, que se renderiza como texto literal sin errores si Templater no está instalado, y se activa automáticamente al instalarlo.
- **Breadcrumbs** — el campo `padre` presente en el frontmatter de casi toda nota curada está listo para usarse como campo "Up" de este plugin en cuanto se instale.

Adicionalmente, el plugin núcleo **Bases** (ya activo, distinto de Dataview, ver `.obsidian/core-plugins.json`) es una vía adicional legítima para construir vistas y agregaciones sobre el frontmatter existente, sin necesidad de un plugin de comunidad. Se menciona aquí como observación disponible, no se implementa salvo pedido explícito del usuario.

## 8. Fuentes de datos vivas (bases de datos externas)

Algunas Fuentes (`Fuentes/`) no son documentos estáticos sino bases de datos externas consultadas en vivo — ej. [[Zam App — Base de datos de autorregistro (Supabase)]], vía MCP de Supabase. Para estas se aplica una extensión de la regla de no-duplicación del §6: **los datos permanecen en su sistema de origen**; el vault nunca almacena filas ni tablas crudas, solo conocimiento sintetizado derivado de ellos — un Patrón, una pieza de Evidencia, o una actualización del Modelo del Usuario — citando en `evidencia_base` la consulta realizada (y el rango de fechas si aplica), nunca los datos en sí. Ver [[Protocolo de Ingesta de Datos Cuantitativos]] para el procedimiento completo de cuándo y cómo se consultan.

## Ver también

[[Arquitectura Cognitiva del Sistema]] · [[Epistemología del Sistema]] · [[Manifiesto del Proyecto - SACP]] · [[Índice]]
