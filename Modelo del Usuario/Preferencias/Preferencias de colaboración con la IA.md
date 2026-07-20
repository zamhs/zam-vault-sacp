---
id: "20260719050501"
tipo: modelo_usuario
subtipo: preferencias
confianza: alta
evidencia_base: ["[[2026-07-19 - Zam comparte contexto extenso para el Modelo del Usuario]]"]
fecha_ultima_actualizacion: 2026-07-19
estado: vigente
tags: [modelo-usuario, preferencias]
relacionado_con: ["[[MOC - Modelo del Usuario]]", "[[Principios operativos]]", "[[Arquitectura Cognitiva del Sistema]]"]
padre: "[[MOC - Modelo del Usuario]]"
---

# Preferencias de colaboración con la IA

## Descripción

Zam fue explícito sobre cómo espera que una IA colabore con él, en dos momentos distintos de la misma conversación (sección de Estilo Cognitivo y sección de Metacognición). Cuando analice un problema, espera que la IA, siempre que sea apropiado:

- Detecte supuestos que él no está cuestionando.
- Identifique puntos ciegos.
- Proponga disciplinas relevantes que quizá no está considerando.
- Genere hipótesis alternativas.
- Diferencie claramente entre hechos, inferencias e hipótesis.
- Señale incertidumbres cuando existan.
- Integre perspectivas de distintos campos.
- Ayude a construir modelos más completos, no solo a resolver la pregunta inmediata.

Durante la metacognición espera, específicamente, que la IA funcione como "supervisor intelectual": que señale sesgos cognitivos, marcos de razonamiento alternativos, evidencia que contradiga sus conclusiones, variables no consideradas, explicaciones más simples o completas, posibles errores metodológicos, y exceso de confianza o conclusiones prematuras. Su frase textual: "No busco una IA que piense por mí, sino una IA que mejore la calidad de mi propio pensamiento."

**Tensión operativa explícita, y la más accionable de todas:** Zam reconoce en la sección de Fortalezas y Limitaciones que su mayor riesgo no suele ser la falta de motivación sino la parálisis por sobreanálisis — su tendencia a expandir el mapa del problema en vez de empezar a recorrerlo. Su instrucción textual: "necesito que mayoría de veces llegues a una conclusión práctica la cual yo pueda ejecutar." Esto matiza todo lo anterior: quiere profundidad y cuestionamiento riguroso, pero no a costa de quedar sin una conclusión ejecutable — el sistema debe balancear exploración exhaustiva con cierre práctico, no solo abrir preguntas indefinidamente.

## Evidencia que sustenta esta observación

Autorreporte directo, declarado en dos secciones distintas y coherentes entre sí, más una advertencia explícita y concreta sobre el riesgo de que el propio estilo de colaboración deseado (cuestionamiento profundo) se vuelva contraproducente si no cierra en algo ejecutable.

## Historial de actualizaciones

- 2026-07-19: creación de la nota a partir de la primera respuesta extensa de Zam.

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

> Justificación para esta nota: Define directamente el comportamiento esperado de la Interfaz Conversacional descrito en `Arquitectura Cognitiva del Sistema.md` — es la instrucción más concreta y operacional de todo el mensaje, y sin registrarla el sistema corre el riesgo de repetir exactamente el patrón que Zam identificó como su mayor riesgo (parálisis por sobreanálisis).
