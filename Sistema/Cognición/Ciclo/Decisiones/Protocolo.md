---
id: "202607190210016"
tipo: motor_cognitivo
motor: Decisiones
subtipo_archivo: protocolo
estado: vigente
tags: [cognicion, motor, metodologia]
relacionado_con: ["[[Arquitectura Cognitiva del Sistema]]", "[[MOC - Cognición]]"]
---

# Protocolo de Decisiones

**Motor anterior:** [[Evidencia/Protocolo|Protocolo de Evidencia]].
**Motor siguiente:** [[Reflexión/Protocolo|Protocolo de Reflexión]].

> Nota de desambiguación: este documento describe el motor cognitivo de Decisiones — el protocolo o metodología que la IA sigue para decidir. Es distinto de la carpeta `/Decisiones/` en la raíz del vault, que contiene las notas atómicas de decisiones reales que el usuario efectivamente tomó. Este motor produce, precisamente, las entradas que terminan viviendo en esa carpeta.

Para estructurar el razonamiento durante este motor puede apoyarse, sin que su uso sea obligatorio, en los marcos recomendados en [[Índice - Marcos de Razonamiento]].

## Los seis pasos

1. **Definir explícitamente qué decisión hay que tomar y qué opciones existen.** Antes de decidir, conviene poner en palabras concretas cuál es la decisión y cuáles son las alternativas reales disponibles, no solo la primera que viene a la mente.

2. **Explorar consecuencias de primer, segundo y tercer orden para cada opción.** Las consecuencias inmediatas rara vez cuentan toda la historia; para cada opción vale la pena pensar qué pasaría después de lo que pasaría después.

3. **Identificar qué sesgos cognitivos podrían estar distorsionando la elección.** Nombrar el sesgo potencial — aversión a la pérdida, anclaje, exceso de confianza, entre otros — ayuda a neutralizar parte de su efecto antes de decidir.

4. **Ponderar la decisión contra el Modelo del Usuario.** La opción técnicamente óptima no siempre es la correcta para esta persona en particular; contrastarla contra sus valores, objetivos y principios documentados evita decisiones desalineadas con quién es.

5. **Tomar la decisión y registrarla en `/Decisiones/` con su justificación y evidencia.** El registro no es un trámite posterior: es parte del protocolo. La decisión se documenta en la carpeta atómica de Nivel 1 junto con el razonamiento y la evidencia que la sostienen.

6. **Marcar explícitamente los supuestos no verificados sobre los que descansa la decisión.** Ninguna decisión se toma con información completa; dejar constancia de qué se está dando por sentado facilita revisarla más adelante si esos supuestos resultan falsos.

Ver también: [[Arquitectura Cognitiva del Sistema]] · [[MOC - Cognición]]
