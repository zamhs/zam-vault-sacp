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
- `dev_tasks` — tareas con prioridad, tiempo límite, vínculo a metas.
- `dev_behavior_logs` — registro estilo TCC: `behavior_id`, `trigger_key` (disparador), `action_key` (acción), `context_key` (contexto), intensidad, calidad. Las claves crudas se traducen a texto humano usando `/Users/macbookair/ZamObsidian/mis_estadisticas/web/lib/behavior-options.ts` (se referencia la ruta, no se copia el contenido, para no desincronizarse si Zam lo edita).
- `dev_gym_sessions`, `dev_gym_set_logs`, `dev_gym_exercises`, `dev_gym_routines`, `dev_routine_exercises` — seguimiento de gimnasio.
- `dev_notes` — notas libres vinculadas a una actividad.
- `dev_goals`, `dev_activities`, `dev_quotes`, `dev_cancelled_days`, `dev_behavior_types` — catálogos/soporte.
- Tablas vacías, fuera de alcance: `dev_skill_nodes`, `dev_achievements`, `dev_achievement_completions`, `dev_snapshots` (restos de una funcionalidad tipo RPG retirada de la UI); `ai_conversations`, `ai_messages` (pertenecían a otro propósito no relacionado con el SACP, según confirmación explícita de Zam).

## Regla de no-duplicación

Consistente con `Convenciones del vault.md` §6 y §8: los datos permanecen en Supabase, su sistema de origen. El vault nunca almacena filas ni tablas crudas — solo síntesis, patrones y actualizaciones del Modelo del Usuario derivadas de un análisis, citando la consulta y el rango de fechas usado (no los datos en sí).

## Fiabilidad estimada

Alta como fuente primaria de comportamiento real (no autorreporte narrado de memoria): son registros hechos por Zam mismo, cerca en el tiempo al evento, de forma estructurada. Limitación conocida: la cobertura depende de su constancia registrando (ej. solo 2 filas en `dev_tasks` al momento de esta ficha, frente a 216 en `dev_behavior_logs`) — la ausencia de datos en una tabla no implica ausencia del comportamiento correspondiente en la vida real.

## Historial de actualizaciones

- 2026-07-19: creación de la ficha. Como parte de la misma sesión de trabajo, se corrigió una vulnerabilidad de seguridad real encontrada en `dev_notes` (Row Level Security desactivado, única tabla del proyecto en ese estado) replicando el patrón de políticas ya usado en el resto de tablas del proyecto.

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
