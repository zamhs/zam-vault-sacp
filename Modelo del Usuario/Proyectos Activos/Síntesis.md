---
id: "202607190240018"
tipo: modelo_usuario
subtipo: sintesis
confianza: n/a
evidencia_base: []
fecha_ultima_actualizacion: 2026-07-19
estado: vigente
tags: [modelo-usuario, sintesis]
relacionado_con: ["[[MOC - Modelo del Usuario]]"]
padre: "[[MOC - Modelo del Usuario]]"
---

# Síntesis - Proyectos Activos

## Regla de no-duplicación

Esta carpeta no contiene notas de contenido propias. Los proyectos del usuario ya viven como notas atómicas de Nivel 1 en `/Proyectos/`, en la raíz del vault. Duplicar esa información aquí crearía dos fuentes de verdad divergentes: una en `/Proyectos/` (donde se crea y edita el contenido real) y otra en `Modelo del Usuario/Proyectos Activos/` (una copia que inevitablemente quedaría desactualizada).

En vez de duplicar, esta nota actúa como punto de síntesis: enlaza conceptualmente hacia `/Proyectos/` y, cuando el usuario instale el plugin Dataview, mostrará aquí mismo una vista filtrada y siempre actualizada de los proyectos activos, sin necesidad de mantener una copia manual.

Esta síntesis enlaza el contenido real que vive en `/Proyectos/`.

## Consulta (inerte hasta instalar Dataview)

El siguiente bloque describe conceptualmente la consulta que debería ejecutarse. Está en un bloque de código de texto plano (no un bloque ```dataview real) para que no falle si el plugin Dataview no está instalado. Cuando el usuario instale Dataview, este bloque debe convertirse en un bloque ```dataview funcional.

```text
FROM "Proyectos" WHERE estado = "activo"
```

## Estado actual

*Pendiente de activar. Esta síntesis se activará como consulta Dataview real en cuanto el plugin esté instalado; mientras tanto, el listado de proyectos activos debe consultarse manualmente en `/Proyectos/`.*

## Notas relacionadas

*(ninguna todavía)*

---
## ¿Por qué vive esto en la memoria permanente?

Pregunta central: ¿Esta información aumentará la capacidad futura del sistema para comprender, razonar o tomar mejores decisiones?

Guía no obligatoria (basta justificar afirmativamente 1-2, no todas):
- ¿Ayuda a construir o mejorar un modelo?
- ¿Conecta conocimientos previamente separados?
- ¿Permite detectar un patrón?
- ¿Será útil para futuras investigaciones?
- ¿Aporta contexto para decisiones futuras?
- ¿Representa un aprendizaje difícil de reconstruir posteriormente?
- ¿Es suficientemente estable como para formar parte del conocimiento de largo plazo?

> Justificación para esta nota: El Modelo del Usuario es la base para toda personalización futura del sistema; esta categoría, aunque vacía hoy, es estructuralmente necesaria para acumular evidencia sobre el usuario a largo plazo.

Ver también: [[MOC - Modelo del Usuario]] · [[Arquitectura Cognitiva del Sistema]]
