---
id: "20260719020200"
tipo: epistemologia
estado: vigente
tags: [arquitectura, epistemologia, fundacional, sacp]
relacionado_con: ["[[Arquitectura Cognitiva del Sistema]]", "[[Manifiesto del Proyecto - SACP]]", "[[MOC - Cognición]]"]
padre: "[[Índice]]"
aliases: [Epistemología, Teoría del Conocimiento del Sistema]
---

# Epistemología del Sistema

Mientras [[Arquitectura Cognitiva del Sistema]] describe los *componentes y el flujo* del sistema, este documento define las *reglas que gobiernan el conocimiento* dentro de ese flujo. Es la teoría del conocimiento que la IA debe aplicar al decidir qué constituye conocimiento válido, cómo evaluar evidencia, y cuándo el conocimiento debe madurar o revisarse.

## 1. Qué considera conocimiento este sistema

El sistema distingue tres niveles:

- **Dato** — una observación cruda, sin interpretar. No vive en la memoria permanente por sí sola.
- **Información** — un dato con contexto que le da significado. Puede vivir temporalmente en `Sistema/Bitácora/` mientras se decide su relevancia.
- **Conocimiento** — información integrada en una estructura, con relaciones a otro conocimiento, que permite explicar o predecir. Solo el conocimiento en este sentido vive en la memoria permanente, como Concepto, Patrón, Hipótesis o Modelo.

Esta distinción es la base del criterio de admisión a la memoria (ver adenda de [[Manifiesto del Proyecto - SACP]] y [[Convenciones del vault]]): un dato aislado no se guarda; un dato que se convierte en conocimiento estructurado, sí.

## 2. Qué considera evidencia

Evidencia es cualquier observación, fuente o dato que incrementa o reduce la confianza en una hipótesis o modelo. No toda evidencia tiene el mismo peso. Como guía orientativa, no como regla rígida:

- Una fuente primaria pesa más que una secundaria.
- Un resultado replicado o consistente en varios casos pesa más que uno anecdótico o aislado.
- Evidencia que sobrevivió un intento genuino de refutación (ver `Sistema/Cognición/Marcos de Razonamiento/Falsación.md`) pesa más que evidencia que solo fue buscada para confirmar.

El campo `evidencia_base` en las notas de `Modelo del Usuario/` y en los Modelos debe listar la evidencia concreta que sostiene la afirmación, no solo la conclusión.

## 3. La escalera dato → concepto → patrón → hipótesis → modelo

- **Dato** — una observación puntual, sin interpretación todavía.
- **Concepto** — una idea o definición estable, suficientemente clara para nombrarse y reutilizarse.
- **Patrón** — una regularidad observada entre varios conceptos o datos a lo largo del tiempo o de varios casos.
- **Hipótesis** — una explicación propuesta y falsable de un patrón. Debe poder estar equivocada.
- **Modelo** — una explicación consolidada que sintetiza múltiples hipótesis, conceptos y patrones, con poder explicativo y predictivo demostrado.

Cada peldaño requiere más evidencia e integración que el anterior. No es obligatorio pasar por todos los peldaños en orden estricto — un Descubrimiento puede generar directamente una Hipótesis — pero la madurez de una pieza de conocimiento se mide por en qué peldaño de esta escalera se encuentra.

## 4. Cuándo una Hipótesis se convierte en Modelo

La promoción de Hipótesis a Modelo no es automática: requiere juicio, pero guiado por criterios explícitos. Una Hipótesis está lista para convertirse en Modelo cuando se cumplen, en conjunto:

- Evidencia convergente proveniente de más de una fuente o caso distinto.
- `confianza: alta` sostenida en el tiempo, no solo en el momento de formularse.
- Uso exitoso de la hipótesis para explicar o predecir en más de un caso.
- Ausencia de contradicciones abiertas sin resolver.

Si falta alguno de estos criterios, la pieza de conocimiento permanece como Hipótesis, no se fuerza su promoción.

## 5. Cuándo un Modelo debe revisarse

Un Modelo entra en revisión cuando ocurre cualquiera de estos disparadores:

- Aparece nueva evidencia que lo contradice.
- Surge un Patrón nuevo que no encaja dentro de su explicación.
- Un Descubrimiento pone en duda alguno de sus componentes.
- Su `fecha_ultima_actualizacion` es muy antigua frente a actividad reciente y relevante en su dominio.

## 6. Cómo se gestionan las contradicciones

Las contradicciones nunca se resuelven sobrescribiendo silenciosamente el conocimiento anterior. El procedimiento es:

1. La contradicción se documenta explícitamente en el campo `contradicciones_conocidas` del Modelo afectado.
2. Se dispara el motor de Investigación o de Evidencia (`Sistema/Cognición/Ciclo/`) para intentar resolverla.
3. Mientras la contradicción permanece abierta, el Modelo se marca `estado: en_revision`.
4. El Modelo solo vuelve a `estado: consolidado` cuando la contradicción se resuelve o se documenta por qué deja de aplicar.

## 7. Cómo se actualiza el conocimiento

La ejecución operativa de la actualización del conocimiento vive en `Sistema/Cognición/Ciclo/Actualización del Conocimiento/Protocolo.md`. Ese protocolo aplica las reglas definidas en este documento — no las duplica. Ante cualquier ambigüedad entre ambos documentos, este documento (Epistemología del Sistema) es la fuente de verdad sobre las reglas; el protocolo de Actualización del Conocimiento es la fuente de verdad sobre el procedimiento paso a paso.

## Ver también

[[Arquitectura Cognitiva del Sistema]] · [[Manifiesto del Proyecto - SACP]] · [[Convenciones del vault]] · [[MOC - Cognición]]
