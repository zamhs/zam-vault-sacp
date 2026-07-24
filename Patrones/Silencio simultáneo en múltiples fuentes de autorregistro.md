---
id: "20260720120001"
tipo: patron
estado: activo
fecha_creacion: 2026-07-20
tags: [patron, datos-cuantitativos]
relacionado_con: ["[[MOC - Patrones]]", "[[Zam App — Base de datos de autorregistro (Supabase)]]", "[[Estado actual — energía, foco y prioridades]]"]
confianza: media
padre: "[[MOC - Patrones]]"
---

# Silencio simultáneo en múltiples fuentes de autorregistro

## Regularidad observada

Cuando Zam deja de registrar en una fuente de autorregistro de la Zam App, no parece ser un evento aislado de esa tabla — coincide con un silencio paralelo en otras fuentes independientes, que no comparten formulario ni momento de captura. En el único caso documentado hasta ahora (julio 2026), tres fuentes distintas de Supabase muestran el mismo corte, casi en la misma fecha:

- `dev_daily_logs` (minutos por actividad — Inglés, Programación, Piano, Marketing, GYM): el último día con las 5 actividades registradas fue **2026-07-08**. Desde entonces, solo dos filas aisladas de GYM (2026-07-10, 2026-07-14) — ninguna de las otras 4 actividades tiene registro en los 12 días previos a este análisis (2026-07-20).
- `dev_behavior_logs`, en los hábitos positivos `skincare`, `meditación`, `creatina`, `sueño`, y en dos negativos con seguimiento de contexto, `procrastinación` e `impulsos`: las cinco últimas filas de estas categorías, sin excepción, son del **2026-07-09**. Cero filas nuevas desde entonces.
- `dev_tasks`: la última tarea fue creada el **2026-07-09**. Cero tareas nuevas desde entonces (de 26 tareas totales desde 2026-05-24).

En contraste, tres categorías siguieron activas durante el mismo período de silencio: `azucar` y `miedo` (comportamientos negativos) y `scroll`, con filas hasta el mismo día de este análisis (2026-07-20), y GYM (con las dos filas sueltas ya mencionadas). Es decir, no es que Zam haya dejado de abrir la app — siguió registrando disparadores de ansiedad/impulso y entrenando — sino que específicamente los hábitos de construcción/mantenimiento (positivos) y la gestión activa de tareas cayeron a la vez, mientras la señal de malestar (azúcar, miedo, scroll) se mantuvo o incluso quedó más visible en proporción.

## Casos que lo sustentan

- Único caso documentado hasta ahora: julio 2026 (arriba). Fuente: consultas SQL de solo lectura vía `execute_sql` sobre `dev_daily_logs`, `dev_behavior_logs` y `dev_tasks` (proyecto Supabase `sjuhxdqcotywuiopjgsr`), agregando por fecha/actividad/comportamiento en el rango 2026-05-24 a 2026-07-20 — ver [[Zam App — Base de datos de autorregistro (Supabase)]]. No se citan filas crudas, solo conteos y fechas agregadas, por `Convenciones del vault.md` §8.

## Posibles excepciones / limitaciones

- N=1 evento: no se sabe todavía si esto es recurrente o un episodio único con una causa puntual. Es notable que el rediseño de captura de datos de la app (activación de `priority`/`due_date`/`goal_id`/`context_key`, `dev_daily_checkins`, etc.) se ejecutó el mismo 2026-07-20 — podría ser tanto síntoma relacionado (Zam notando la caída y respondiendo) como coincidencia.
- No hay causalidad establecida entre el silencio en hábitos positivos/tareas y la continuidad de azúcar/miedo/scroll — es una correlación temporal observada, no una explicación. Tampoco se puede distinguir con estos datos si el comportamiento real cesó o si solo cesó el registro (ver limitación ya documentada en la Fuente: la ausencia de datos no implica ausencia del comportamiento).
- El volumen total es bajo (219 filas de `dev_behavior_logs` en ~2 meses) — un solo período de silencio de 10-12 días pesa proporcionalmente mucho en la serie completa.

## Historial de actualizaciones

- 2026-07-23: seguimiento de solo lectura sobre las mismas tres tablas, con el rango extendido hasta hoy. El silencio en `dev_daily_logs` para las 4 actividades núcleo (Programación, Inglés, Piano, Marketing) **no se resolvió**: se extiende ya a 15 días consecutivos sin ninguna fila nueva (último registro sigue siendo 2026-07-08), mientras GYM se mantiene activo (3 sesiones en los últimos 14 días, la más reciente 2026-07-22). En cambio, `dev_behavior_logs` sí se recuperó: las categorías que estaban en silencio el 2026-07-20 (`meditación`, `orden`, `skincare`, `sueño`, `impulsos`, `procrastinación`) tienen registro hasta el día de hoy. `dev_tasks` registró su primera fila nueva desde 2026-07-09 recién el 2026-07-22, rompiendo 13 días de inactividad. Esto refina, no reemplaza, la hipótesis original: el silencio no fue un evento ya superado, sino que se concentró específicamente en la dimensión de `dev_daily_logs` más directamente ligada a las prioridades declaradas el 2026-07-19 (construcción de habilidades), mientras el resto del sistema de autorregistro (hábitos, malestar, tareas, gimnasio) sí muestra actividad reciente. Se mantiene `confianza: media`: sigue siendo la misma ventana de silencio observada y no una segunda ocurrencia independiente; subir a `alta` requeriría ver el patrón repetirse en un período distinto y separado.
- 2026-07-23: posible recurrencia del mismo patrón dentro de la herramienta diseñada para prevenirlo. `dev_daily_checkins` (mood/energy/stress diario), activa desde 2026-07-20, tiene una sola fila registrada en sus primeros 4 días de existencia (2026-07-22: mood 2/5, energy 2/5, stress 4/5, nota de sueño interrumpido). N demasiado bajo para conclusión propia, pero se documenta aquí porque es exactamente el tipo de señal temprana que esa tabla se diseñó para capturar — ver referencia cruzada en [[Estado actual — energía, foco y prioridades]].

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

> Justificación para esta nota: Conecta tres tablas independientes de la Zam App que ningún análisis previo había cruzado, y es exactamente el tipo de señal de riesgo temprano que el SACP se propuso poder anticipar (ver Adenda del Manifiesto). Si no se registra ahora, este episodio específico se diluirá en filas futuras y será imposible de reconstruir con esta granularidad — la próxima vez que aparezca un patrón similar, esta nota es lo que permite reconocerlo como recurrencia en vez de descubrirlo desde cero.
