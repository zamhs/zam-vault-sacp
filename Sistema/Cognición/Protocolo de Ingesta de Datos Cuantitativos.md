---
id: "20260719060102"
tipo: integracion_datos
estado: vigente
tags: [cognicion, integracion-datos, datos-cuantitativos]
relacionado_con: ["[[Arquitectura Cognitiva del Sistema]]", "[[MOC - Cognición]]", "[[Zam App — Base de datos de autorregistro (Supabase)]]", "[[Epistemología del Sistema]]"]
---

# Protocolo de Ingesta de Datos Cuantitativos

Capacidad transversal, invocable desde cualquier motor del Ciclo (principalmente Evidencia e Investigación) o directamente desde la Interfaz Conversacional. No es una etapa más del Ciclo ni un cuarto eje de `Sistema/Cognición/` — es una extensión puntual que da a los motores existentes acceso a datos conductuales reales de Zam, en vivo, en vez de depender solo de autorreporte narrado en conversación.

## Por qué existe

Conecta directamente con el objetivo final del SACP tal como Zam lo precisó (ver la Adenda correspondiente en [[Manifiesto del Proyecto - SACP]]): construir un modelo cada vez más preciso de cómo piensa, aprende y actúa Zam, capaz de **anticipar riesgos, detectar patrones invisibles y proponer intervenciones antes de que aparezcan los problemas**. Los datos de [[Zam App — Base de datos de autorregistro (Supabase)]] — en particular `dev_behavior_logs`, con su estructura disparador/acción/contexto estilo TCC — son insumo directo para ese objetivo: son el mecanismo real de "qué desencadena mis hábitos", no una descripción posterior de memoria.

## Cuándo se activa

Ambos modos, sin preferencia entre ellos (decisión explícita de Zam):

- **Bajo pedido explícito**: Zam pide revisar sus datos, su progreso, sus hábitos, etc.
- **Proactivamente**: la conversación toca un tema donde evidencia cuantitativa real cambiaría la calidad de la respuesta — hábitos, conductas, disciplina, progreso de gimnasio, cumplimiento de tareas/metas — y depender solo de autorreporte sería una respuesta más débil que consultar el dato real disponible.

## Cómo se consulta

- Herramientas MCP de Supabase ya conectadas en este entorno, `project_id: sjuhxdqcotywuiopjgsr`.
- Siempre consultas `SELECT` de solo lectura vía `execute_sql`. Nunca `INSERT`/`UPDATE`/`DELETE`/`apply_migration` sobre este proyecto salvo pedido explícito de Zam en la conversación misma.
- El diccionario de claves de `dev_behavior_logs` (trigger/action/context) vive en `/Users/macbookair/ZamObsidian/mis_estadisticas/web/lib/behavior-options.ts` — se consulta esa ruta para traducir claves crudas a texto humano antes de razonar sobre ellas.

## Qué se hace con el resultado

Cada fila devuelta es un *dato*, el primer peldaño de la escalera epistemológica (ver [[Epistemología del Sistema]] §3: dato → concepto → patrón → hipótesis → modelo). Nunca se pegan filas o tablas crudas al vault — el detalle vivo se vuelve a consultar cuando haga falta, no se archiva.

## Cuándo asciende a memoria permanente

Solo si el análisis del dato consultado revela algo que anticipa un riesgo, expone un patrón antes invisible, o sugiere una intervención concreta — el criterio de valor más alto declarado en la Adenda del Manifiesto — y además pasa el criterio de admisión estándar (`Convenciones del vault.md` §4). En la práctica, esto toma una de tres formas:

- Un **Patrón** nuevo en `Patrones/`.
- Una pieza de **Evidencia** para una Hipótesis ya existente (ej. [[Riesgo de repetición de patrones familiares por proximidad estructural]]).
- Una **actualización** de una nota de `Modelo del Usuario/` (ej. Hábitos, Estado Actual, Fortalezas/Limitaciones).

La nota resultante cita en `evidencia_base` la consulta realizada y el rango de fechas usado — nunca los datos crudos, siguiendo `Convenciones del vault.md` §8.

## Relación con el Ciclo

Alimenta principalmente los motores de **Evidencia** y **Actualización del Conocimiento**. Puede disparar **Investigación** si un dato resulta sorprendente o contradice lo ya asumido sobre Zam en el Modelo del Usuario.

## Excepción de escritura: flujo de Tareas Asignadas (`dev_tasks` / `dev_notes`)

Desde el 3 de agosto de 2026, existe una excepción acotada y explícita a la regla de solo lectura de esta sección, configurada por Zam mismo (vía Claude Code) con una sección correspondiente en la app (`/tareas`) para ver y completar lo que se le asigne. Aplica únicamente a `dev_tasks` y `dev_notes`, y únicamente bajo pedido explícito de Zam dentro de la conversación — nunca de forma proactiva ni automatizada (no hay cron ni disparador fuera de la conversación).

Flujo:

1. Zam pide una tarea de un área (ej. "dame una tarea de inglés"). Antes de proponerla, se consultan las `dev_notes` más recientes y las `dev_tasks` completadas recientes del mismo `activity_id`, para dar continuidad real y no repetir ni generar algo genérico.
2. Se inserta una fila nueva en `dev_tasks`: `completed=false`, `title` específico, `activity_id`, `priority`, opcionalmente `due_date`/`goal_id`, `notes` (el motivo de por qué se eligió esa tarea), `estimated_minutes`.
3. Cuando Zam reporta que terminó — tiempo tardado, cómo se sintió (`quality`, 1-10), nota opcional — se actualiza esa misma fila: `completed=true`, `completed_at`, `completed_date`, `elapsed_seconds`, `quality`, y si hay nota de cierre se concatena a `notes` con el separador `\n\n— Cierre: ...` — nunca se borra el contexto original.
4. Si Zam lo pide al final de la sesión, se inserta un resumen en `dev_notes` (`title`, `body`, `activity_id`, `start_date` = hoy) — es lo que da continuidad a la siguiente sesión de esa misma área, dado que no hay memoria entre chats distintos.
5. `dev_todos` queda fuera de este flujo — es para pendientes sueltos sin área ni métricas; `dev_tasks` es la tabla correcta para tareas asignadas por una IA con seguimiento de calidad y tiempo.

Claude Code puede operar el mismo flujo sobre la misma base de datos — filas o notas que no se generaron en esta conversación pueden venir de ahí, bajo el mismo protocolo.

Todo lo demás en `dev_tasks`/`dev_notes` fuera de este flujo específico, y el resto de las tablas del proyecto, permanecen bajo la regla general de solo lectura de esta sección.

## Ver también

[[Zam App — Base de datos de autorregistro (Supabase)]] · [[Arquitectura Cognitiva del Sistema]] · [[MOC - Cognición]] · [[Epistemología del Sistema]] · [[Índice]]
