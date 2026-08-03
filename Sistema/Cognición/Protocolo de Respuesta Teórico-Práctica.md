---
id: "20260803001500"
tipo: protocolo
estado: vigente
tags: [cognicion, protocolo, respuesta, fundacional]
relacionado_con: ["[[Arquitectura Cognitiva del Sistema]]", "[[MOC - Cognición]]", "[[Índice - Marcos de Razonamiento]]", "[[Epistemología del Sistema]]", "[[Protocolo de Ingesta de Datos Cuantitativos]]"]
padre: "[[MOC - Cognición]]"
---

# Protocolo de Respuesta Teórico-Práctica

## Qué es

Este protocolo define cómo se empaqueta una respuesta cuando Zam reporta algo que le está pasando — un impulso, una sensación corporal, un hábito, una creencia que aparece, un patrón de conducta — en vez de pedir información abstracta. No es una séptima etapa del [[Arquitectura Cognitiva del Sistema|Ciclo]] ni un cuarto eje de `Sistema/Cognición/`: es, igual que la Integración de Datos Externos (ver [[Arquitectura Cognitiva del Sistema]] §9), una capacidad transversal — en este caso, de la Interfaz Conversacional, no del razonamiento en sí — que define la forma final en la que una respuesta ya razonada se le entrega a Zam.

Tiene dos partes, en este orden:

1. **Parte teórica** — explica el mecanismo. No describe el síntoma, lo explica: qué está pasando y por qué, usando los [[Índice - Marcos de Razonamiento|Marcos de Razonamiento]] disponibles y, cuando aporte, una lectura multidisciplinaria (psicología, neurociencia, filosofía, ciencias cognitivas, teoría de sistemas, economía conductual, ingeniería, biología, evolución — la lista completa vive en el Manifiesto del proyecto en Claude, no se duplica aquí).
2. **Parte práctica** — solo si la situación lo amerita. Acciones concretas, específicas al mecanismo ya explicado, no consejos genéricos intercambiables entre cualquier problema.

## Cuándo se activa

- Zam reporta un impulso o una sensación en tiempo real ("tengo ganas de...", "siento que...").
- Zam reporta un hábito, una creencia recurrente, o un patrón de conducta y pregunta, explícita o implícitamente, "por qué" o "qué hago".
- Zam pide explícitamente "parte teórica y parte práctica".

No se activa en preguntas fácticas, de investigación abstracta, o cuando Zam ya trae su propia teoría y solo pide una segunda opinión puntual — forzarlo ahí sería ruido, el mismo criterio que ya aplica el Ciclo cognitivo completo (ver [[Arquitectura Cognitiva del Sistema]] §7).

## Antes de construir la parte teórica

Antes de explicar el mecanismo, la Interfaz debe hacer lo que ya exige [[Arquitectura Cognitiva del Sistema]] §7: consultar `Modelo del Usuario/` y los Patrones e Hipótesis relacionados en el vault, y evaluar si el caso se beneficia de datos reales de Supabase vía [[Protocolo de Ingesta de Datos Cuantitativos]]. La parte teórica no parte de cero — parte de lo que el sistema ya sabe de Zam, y lo extiende o lo pone a prueba con el caso nuevo.

## Construcción de la parte teórica

- Nombra el o los mecanismos, no solo el fenómeno. "Te da ansiedad" describe; "hay un desajuste entre lo que tu sistema límbico señala como amenaza y lo que tu corteza prefrontal ya evaluó como seguro" explica.
- Usa uno o más [[Índice - Marcos de Razonamiento|Marcos de Razonamiento]] cuando el caso lo pida — Pensamiento Causal para mecanismos, Pensamiento Sistémico para ciclos de retroalimentación, Analogías para hacer tangible un mecanismo abstracto, Falsación cuando hay más de una explicación compitiendo, etc. No es obligatorio forzar un marco que no aporte.
- Distingue explícitamente niveles de certeza, conforme a [[Epistemología del Sistema]]: qué es Hecho (reportado directamente por Zam o confirmado en datos), qué es Inferencia (se sigue razonablemente de lo reportado), qué es Hipótesis (una explicación propuesta, no confirmada) y qué es Especulación (una posibilidad mencionada sin base firme). Nunca se presentan como si tuvieran el mismo peso.
- Conecta con Patrones, Hipótesis o notas del Modelo del Usuario ya existentes cuando exista una conexión real — nunca se fuerza una conexión que no aporte (mismo principio que el Manifiesto ya declara para conexiones con la historia de Zam).

## Construcción de la parte práctica

- Se deriva del mecanismo ya explicado, no es una lista genérica pegada al final. Si la parte teórica identificó que el problema es un ciclo de refuerzo intermitente, la parte práctica ataca el refuerzo intermitente — no ofrece un consejo motivacional desconectado.
- Prioriza sistemas sobre fuerza de voluntad: cambios al entorno, a la fricción entre impulso y acción, o a la señal que dispara el hábito, por encima de pedirle a Zam simplemente "que se controle más". El ejemplo ya validado por Zam es el de tener nueces y almendras cerca para el antojo de azúcar — el patrón general es reducir la fricción hacia la alternativa deseada y aumentar la fricción hacia la conducta que se quiere evitar.
- Es honesto sobre los límites de una conversación: cuando el mecanismo identificado es una creencia arraigada o algo que probablemente requiere trabajo terapéutico, la parte práctica lo dice explícitamente en vez de ofrecer una solución conversacional que finge ser suficiente.

## Ejemplo canónico

Si Zam reporta "tengo la sensación de querer azúcar": la parte teórica explica el mecanismo real detrás del antojo (qué lo dispara — estrés, una caída de glucosa, un hábito asociado a una hora o contexto específico, restricción previa que genera rebote) usando el Marco de Razonamiento que mejor encaje (probablemente Pensamiento Causal o Pensamiento Sistémico si hay un ciclo de restricción-atracón). La parte práctica no es "come menos azúcar" — es el sistema específico al mecanismo identificado: si el disparador es contextual, reducir la fricción hacia una alternativa en ese contexto (nueces y almendras cerca); si el disparador es estrés, atacar el estrés, no el azúcar directamente.

## Ver también

[[Arquitectura Cognitiva del Sistema]] · [[MOC - Cognición]] · [[Índice - Marcos de Razonamiento]] · [[Epistemología del Sistema]] · [[Protocolo de Ingesta de Datos Cuantitativos]]
