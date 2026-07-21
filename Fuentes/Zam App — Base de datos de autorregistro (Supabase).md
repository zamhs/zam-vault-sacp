---
id: "20260719060101"
tipo: fuente
estado: activo
fecha_creacion: 2026-07-19
tags: [fuente, datos-cuantitativos, autorregistro]
relacionado_con: ["[[MOC - Fuentes]]", "[[Protocolo de Ingesta de Datos Cuantitativos]]", "[[Arquitectura Cognitiva del Sistema]]"]
autor: Zam
tipo_fuente: primaria
url: "https://zam-app-2026.vercel.app/"
padre: "[[MOC - Fuentes]]"
---

# Zam App — Base de datos de autorregistro (Supabase)

## Resumen

Aplicación web personal de Zam (Next.js + Supabase, sin capa de API propia — acceso cliente-directo) donde autorregistra datos cuantitativos de su vida diaria: hábitos, conductas (seguimiento estilo TCC de disparadores/acciones/contexto), sesiones de gimnasio, tareas, metas y notas libres. Código fuente en `/Users/macbookair/ZamObsidian/mis_estadisticas/web/`.

Es una **base de datos viva**, no un documento estático: sus filas cambian constantemente conforme Zam la usa. Esta ficha no es una copia de esos datos — documenta *cómo acceder a ellos*, no su contenido (ver "Regla de no-duplicación" más abajo).

## Cómo se accede

El servidor MCP de Supabase ya conectado en este entorno (`mcp__supabase__*`) apunta exactamente al proyecto correcto: `sjuhxdqcotywuiopjgsr` ("ZAM Desarrollo Personal"). Esto se verificó de forma independiente — no solo confiando en la configuración local del repo, sino extrayendo el bundle JS servido en vivo por `https://zam-app-2026.vercel.app/inicio` y confirmando que ese mismo ref de proyecto está inlineado en el código realmente desplegado.

**Regla de acceso: solo lectura.** Desde este sistema se usa exclusivamente `execute_sql` con consultas `SELECT`. Nunca se ejecuta `INSERT`/`UPDATE`/`DELETE`/`apply_migration` sobre este proyecto salvo pedido explícito de Zam en la conversación (la única excepción documentada es la corrección de seguridad de RLS descrita en `Historial de actualizaciones`, aplicada una sola vez con su aprobación).

Ver el procedimiento completo de cuándo y cómo consultar esta fuente en [[Protocolo de Ingesta de Datos Cuantitativos]].

## Esquema resumido

Todas las tablas de datos reales usan el prefijo `dev_` (esquema en uso activo, no un entorno de pruebas huérfano):

- `dev_daily_logs` — minutos/calidad/identity_score por actividad y día.
- `dev_tasks` — tareas con `priority` (alta/media/baja), `due_date` y `goal_id` (vínculo a `dev_goals`), más tiempo límite. Soporta dos modos de captura: registrar una tarea ya hecha (retroactivo) o planificarla (`completed:false`, sin fecha de finalización) — permite medir procrastinación real (brecha `due_date` vs `completed_at`), no solo trabajo ya terminado. **Ver nota de fecha de corte abajo: antes del 2026-07-20 estos tres campos no eran señal real.**
- `dev_behavior_logs` — registro estilo TCC: `behavior_id`, `trigger_key` (disparador), `action_key` (acción), `context_key` (contexto — vértice único, un solo comportamiento por fila), `context_keys` (jsonb, lista de contextos — para comportamientos con contexto múltiple como `scroll`; reemplaza un hack anterior que codificaba esta misma información como JSON dentro de `notes`), intensidad, calidad, `notes` (texto libre genuino, opcional). Las claves crudas se traducen a texto humano usando `/Users/macbookair/ZamObsidian/mis_estadisticas/web/lib/behavior-options.ts` (se referencia la ruta, no se copia el contenido, para no desincronizarse si Zam lo edita). **Ver nota de fecha de corte: antes del 2026-07-20, `context_key` no se llenaba nunca (campo muerto) y `notes` en filas de `scroll` contenía JSON estructurado, no texto libre.**
- `dev_daily_checkins` — tabla nueva (2026-07-20): estado transversal del día independiente de cualquier actividad puntual — `mood`, `energy`, `stress` (escala 1-5), `notes`. Una fila por día (`date` único, upsert). Pensada para capturar señal incluso en días sin ningún hábito logueado, que es justo la señal de riesgo más relevante.
- `dev_gym_sessions`, `dev_gym_set_logs` (incluye `rpe`, escala 6-10, opcional por set — agregado 2026-07-20), `dev_gym_exercises`, `dev_gym_routines`, `dev_routine_exercises` — seguimiento de gimnasio.
- `dev_notes` — notas libres vinculadas a una actividad.
- `dev_goals` (incluye `due_date`, activado 2026-07-20 — antes de esa fecha siempre era `null`), `dev_activities`, `dev_quotes`, `dev_cancelled_days`, `dev_behavior_types` — catálogos/soporte.
- Tablas vacías, fuera de alcance: `dev_skill_nodes`, `dev_achievements`, `dev_achievement_completions`, `dev_snapshots` (restos de una funcionalidad tipo RPG retirada de la UI); `ai_conversations`, `ai_messages` (pertenecían a otro propósito no relacionado con el SACP, según confirmación explícita de Zam).

### Fecha de corte de campos recién activados (2026-07-20)

Varios campos existían en el esquema desde antes pero nunca se llenaban desde ningún formulario — peor que `NULL` para análisis automatizado, porque un valor constante falso simula señal donde no la hay. El 2026-07-20 se activaron en la UI real:
- `dev_tasks.priority` — antes siempre `'media'` (hardcodeado), ahora refleja selección real.
- `dev_tasks.due_date` y `dev_tasks.goal_id` — antes siempre `null`, ahora opcionales pero reales cuando están presentes.
- `dev_goals.due_date` — antes siempre `null`.
- `dev_behavior_logs.context_key` — antes nunca se escribía pese a estar en el schema.

**Cualquier fila con `created_at` anterior a 2026-07-20 en `dev_tasks` o `dev_goals` debe tratarse como si estos campos fueran `NULL`, sin importar el valor constante que muestren** — no son señal real, son un artefacto de la implementación previa. No se corrigieron retroactivamente para no fabricar historia que Zam nunca declaró.

## Regla de no-duplicación

Consistente con `Convenciones del vault.md` §6 y §8: los datos permanecen en Supabase, su sistema de origen. El vault nunca almacena filas ni tablas crudas — solo síntesis, patrones y actualizaciones del Modelo del Usuario derivadas de un análisis, citando la consulta y el rango de fechas usado (no los datos en sí).

## Fiabilidad estimada

Alta como fuente primaria de comportamiento real (no autorreporte narrado de memoria): son registros hechos por Zam mismo, cerca en el tiempo al evento, de forma estructurada. Limitación conocida: la cobertura depende de su constancia registrando (ej. solo 2 filas en `dev_tasks` al momento de esta ficha, frente a 216 en `dev_behavior_logs`) — la ausencia de datos en una tabla no implica ausencia del comportamiento correspondiente en la vida real.

## Historial de actualizaciones

- 2026-07-19: creación de la ficha. Como parte de la misma sesión de trabajo, se corrigió una vulnerabilidad de seguridad real encontrada en `dev_notes` (Row Level Security desactivado, única tabla del proyecto en ese estado) replicando el patrón de políticas ya usado en el resto de tablas del proyecto.
- 2026-07-20: rediseño de captura de datos ejecutado a pedido de Zam, con el criterio explícito de mejorar el análisis del SACP (ver [[Adenda del Manifiesto]] / objetivo de modelar disparadores, emociones y disciplina). Cambios de esquema: activación de `dev_tasks.priority/due_date/goal_id` y `dev_goals.due_date` (antes campos muertos con valor constante falso — ver "Fecha de corte" arriba); activación de `dev_behavior_logs.context_key`; tabla nueva `dev_daily_checkins` (mood/energy/stress diarios); columna nueva `dev_behavior_logs.context_keys` (jsonb) reemplazando un hack de JSON-en-`notes` usado por el comportamiento `scroll`, con backfill del histórico; `notes` liberado como texto libre genuino en todos los behavior logs; columna nueva `dev_gym_set_logs.rpe` (esfuerzo percibido por set, 6-10). **Nota de proceso:** el código de la app se actualizó primero; las migraciones DDL sobre `sjuhxdqcotywuiopjgsr` (creación de `dev_daily_checkins`, `ALTER TABLE` de `context_keys` y `rpe` + backfill) se aplican en una sesión separada por una interrupción temporal de herramientas — si esta ficha se consulta antes de que ese paso se confirme, verificar con `list_tables`/`execute_sql` si las columnas/tabla ya existen antes de asumir que los campos nuevos tienen datos.
- 2026-07-20 (misma sesión, más tarde): las 3 migraciones pendientes mencionadas arriba se aplicaron (`apply_migration`, confirmadas por `get_advisors` y por `information_schema.columns`/`to_regclass`). El backfill de `context_keys` para `scroll` resultó ser un no-op real: de las 15 filas históricas de `scroll`, ninguna tenía JSON-en-`notes` (0 filas con `notes` no nulo) — se documenta para que no se reintente. Acto seguido se ejecutó por primera vez el [[Protocolo de Ingesta de Datos Cuantitativos]] completo (consultas de solo lectura sobre `dev_daily_logs`, `dev_behavior_logs`, `dev_tasks`, `dev_goals`, `dev_gym_sessions`/`dev_gym_set_logs`, rango 2026-05-24 a 2026-07-20). Resultado principal: [[Silencio simultáneo en múltiples fuentes de autorregistro]] (nueva nota en `Patrones/`), con referencia cruzada añadida a [[Estado actual — energía, foco y prioridades]]. Otros hallazgos de esa pasada quedan documentados aquí porque no cruzaron el umbral de admisión como nota propia, para que la próxima sesión no repita el diagnóstico desde cero: (a) `dev_tasks` sigue prácticamente sin uso (26 filas totales, todas con `created_at` anterior al corte del 2026-07-20, 0 tareas nuevas desde 2026-07-09) — confirma, no amplía, lo ya anticipado en el plan de rediseño; (b) el fill-rate de `trigger_key`/`action_key`/`context_key` en `dev_behavior_logs` sigue bajo incluso donde el campo ya estaba activo antes de esta sesión (0% en `miedo`, `sueño`, `skincare`, `meditación`, `creatina`, `scroll`; parcial en `azucar`, `procrastinación`, `impulsos`, `orden`) — este hallazgo no generó nota nueva porque ya había motivado directamente la decisión de diseño de la Fase 2 (indicador de registro incompleto), no es un hallazgo nuevo sino la cuantificación de una decisión ya tomada; (c) la progresión de carga en `dev_gym_set_logs` (por ejercicio, mayo–julio 2026) es consistente y positiva en la mayoría de ejercicios con ≥5 sets registrados, pero no se consideró suficientemente no-obvia para admisión — es la señal que la propia app ya expone al usuario vía `fetchPrevSets()`.

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

> Justificación para esta nota: Sin documentar este acceso, la capacidad de consultar datos conductuales reales de Zam existiría solo dentro de esta conversación y se perdería en la siguiente — esta ficha la hace descubrible y reutilizable en cualquier conversación futura donde el MCP de Supabase siga conectado.
