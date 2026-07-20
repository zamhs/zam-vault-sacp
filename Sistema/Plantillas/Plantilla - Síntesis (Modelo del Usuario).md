---
id: <% tp.date.now("YYYYMMDDHHmmss") %>
tipo: modelo_usuario
subtipo: sintesis
confianza: n/a
evidencia_base: []
fecha_ultima_actualizacion: <% tp.date.now("YYYY-MM-DD") %>
estado: vigente
relacionado_con: []
padre: "[[MOC - Modelo del Usuario]]"
---

# <% tp.file.title %>

## Qué es esta nota

Las notas de síntesis dentro de `Modelo del Usuario/` no duplican contenido que ya vive en otra carpeta del vault (por ejemplo `/Proyectos/`, `/Decisiones/`, `/Conversaciones/`). En vez de copiar información, esta nota sintetiza y apunta hacia esas notas originales, describiendo el patrón agregado que emerge al observarlas en conjunto.

## Patrón sintetizado

## Notas fuente relevantes

A modo de referencia inerte, el tipo de consulta que describe conceptualmente qué notas alimentan esta síntesis (no es una consulta Dataview real, solo ilustra el patrón):

```text
FROM "<Carpeta>" WHERE <condición>
```

Ejemplo: `FROM "Proyectos" WHERE estado = "activo"` para sintetizar cómo se comporta el usuario frente a proyectos activos, sin duplicar cada nota de proyecto aquí.

## Historial de actualizaciones

Ver también: [[Índice]]

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

> Justificación para esta nota:
