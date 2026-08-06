---
id: "20260806073500"
tipo: integracion_datos
estado: vigente
tags: [cognicion, integracion-datos, tareas, dev-tasks]
relacionado_con: ["[[Protocolo de Ingesta de Datos Cuantitativos]]", "[[Zam App — Base de datos de autorregistro (Supabase)]]", "[[MOC - Cognición]]", "[[Arquitectura Cognitiva del Sistema]]"]
---

# Protocolo de Asignación de Tareas Personalizadas

Capacidad transversal, invocable desde cualquier motor del Ciclo o directamente desde la Interfaz Conversacional, **bajo pedido explícito de Zam únicamente** — nunca automática, sin cron, sin tarea programada de Claude Code. A diferencia de [[Protocolo de Ingesta de Datos Cuantitativos]] (solo lectura), este protocolo **sí implica escritura** (`INSERT`/`UPDATE`) sobre `dev_tasks` y `dev_notes`.

## Por qué existe

Zam practica habilidades (ej. inglés) en chats sueltos de Claude.ai, un producto sin memoria compartida con Claude Code — cada sesión nueva empieza en blanco. La personalización día a día ("qué le falta", "en qué se quedó") no puede depender de que la IA recuerde chats pasados, porque no puede. Depende de que cada sesión relevante quede registrada en Supabase de forma estructurada, y de que la IA la consulte antes de asignar la siguiente tarea. **Supabase es la memoria persistente entre sesiones de chat** — tanto de Claude Code como de Claude.ai, que comparten el mismo conector al proyecto `sjuhxdqcotywuiopjgsr`.

## Cuándo se activa — el flujo

1. Zam pide una tarea de un área (ej. "dame una tarea de inglés") en cualquier chat con el conector de Supabase.
2. La IA consulta primero `dev_notes` (últimas filas con ese `activity_id`) y `dev_tasks` completadas recientes del mismo `activity_id`, para saber en qué se quedó.
3. Inserta una fila nueva en `dev_tasks`: `completed=false`, `title` específico y personalizado (nunca genérico), `activity_id`, `priority`, `due_date`/`goal_id` opcionales, `notes` (contexto de por qué se eligió esa tarea), `estimated_minutes`.
4. Zam hace la tarea y la completa — por chat (reportando minutos, calidad 1-10 y una nota opcional) o directamente en `/tareas` en la app. Se actualiza la fila: `completed=true`, `completed_at`, `completed_date`, `elapsed_seconds`, `quality`, `notes`.
5. Al cierre de la sesión, a pedido de Zam, la IA inserta un resumen en `dev_notes` (`title`, `body`, `activity_id`, `start_date=hoy`).
6. La próxima vez que se pide tarea de esa misma área, se repite el paso 2 — el ciclo se retroalimenta y las tareas se vuelven cada vez más específicas.

## Regla de continuidad

Nunca asignar una tarea de un área sin antes consultar `dev_notes` + `dev_tasks` completadas recientes de ese `activity_id`. El objetivo es dar continuidad real ("en qué nos quedamos", qué falta mejorar), no repetir contenido ni ser genérico.

## Dónde se ejecuta

Tanto desde Claude Code como desde Claude.ai (chat normal) — ambos con el mismo conector de Supabase sobre `sjuhxdqcotywuiopjgsr`. Este vault documenta el protocolo, pero la fuente de verdad operativa vive en Supabase mismo: la migración `add_quality_to_tasks` agregó `COMMENT ON TABLE/COLUMN` a `dev_tasks` y `dev_notes` como red de seguridad para una sesión de chat que tenga el conector pero no acceso a este vault.

## Diferencia con `dev_todos`

No usar `dev_todos` para esto — esa tabla es para pendientes sueltos sin `activity_id` ni métricas de tiempo/calidad. `dev_tasks` es la tabla correcta porque ya tiene todos los campos necesarios (`activity_id`, `priority`, `due_date`, `goal_id`, `estimated_minutes`, `elapsed_seconds`, `quality`, `notes`).

## Relación con el Ciclo

Análoga a la de [[Protocolo de Ingesta de Datos Cuantitativos]] — alimenta **Evidencia** y **Actualización del Conocimiento**. A diferencia de aquel, aquí hay escritura activa, por lo que también se relaciona con **Decisiones**: la IA decide qué tarea específica asignar a partir del historial consultado.

## Ver también

[[Protocolo de Ingesta de Datos Cuantitativos]] · [[Zam App — Base de datos de autorregistro (Supabase)]] · [[MOC - Cognición]] · [[Arquitectura Cognitiva del Sistema]] · [[Índice]]

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

> Justificación para esta nota: sin documentar este protocolo, la capacidad de asignar tareas personalizadas con continuidad real existiría solo dentro de esta conversación y se perdería en la siguiente — esta nota la hace descubrible y ejecutable en cualquier chat futuro (Claude Code o Claude.ai) donde el conector de Supabase siga disponible.
