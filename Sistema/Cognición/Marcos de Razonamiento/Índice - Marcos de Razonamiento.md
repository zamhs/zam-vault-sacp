---
id: "20260719022011"
tipo: indice
estado: vigente
tags: [cognicion, marco-razonamiento]
relacionado_con: ["[[Arquitectura Cognitiva del Sistema]]", "[[MOC - Cognición]]"]
padre: "[[MOC - Cognición]]"
---

# Índice - Marcos de Razonamiento

## Qué es esta carpeta
Los Marcos de Razonamiento son una **caja de herramientas metodológica**, no una etapa más del ciclo cognitivo. No son secuenciales ni obligatorios: la IA los selecciona y combina según la naturaleza del problema que está resolviendo *dentro* de cualquier motor del ciclo (Investigación → Hipótesis → Evidencia → Decisiones → Reflexión → Actualización del Conocimiento, definido en `Sistema/Cognición/Ciclo/`).

Un mismo motor puede requerir un solo marco, varios combinados, o ninguno en particular — la elección depende del tipo de problema, no de una regla fija. Esta carpeta documenta qué herramientas hay disponibles y da referencias de qué marcos suelen encajar mejor con cada motor, a modo de sugerencia y no de prescripción.

## Marcos recomendados (no obligatorios) por motor del ciclo

| Motor del ciclo | Marcos recomendados | Protocolo del motor |
|---|---|---|
| Investigación | [[Primeros Principios]], [[Descomposición]], [[Pensamiento Sistémico]] | [[Protocolo]] (Investigación) |
| Hipótesis | [[Abducción]], [[Analogías]], [[Pensamiento Causal]], [[Pensamiento Contrafactual]] | [[Protocolo]] (Hipótesis) |
| Evidencia | [[Falsación]], [[Pensamiento Bayesiano]] | [[Protocolo]] (Evidencia) |
| Decisiones | [[Pensamiento Sistémico]], [[Pensamiento Contrafactual]], [[Modelado]] | [[Protocolo]] (Decisiones) |
| Reflexión | [[Pensamiento Sistémico]], cualquiera aplicado en retrospectiva | [[Protocolo]] (Reflexión) |
| Actualización del Conocimiento | [[Pensamiento Bayesiano]], [[Modelado]] | [[Protocolo]] (Actualización del Conocimiento) |

> Nota: los enlaces "Protocolo" de la tabla apuntan al archivo `Protocolo.md` dentro de la carpeta de cada motor en `Sistema/Cognición/Ciclo/<Motor>/`. Obsidian resolverá el wikilink correcto según la carpeta de origen de cada nota (cada motor tiene su propio `Protocolo.md`).

## Los 10 marcos disponibles
- [[Pensamiento Causal]] — relaciones causa-efecto, más allá de la correlación.
- [[Pensamiento Sistémico]] — partes interrelacionadas con retroalimentación, no eventos aislados.
- [[Primeros Principios]] — descomponer hasta verdades básicas y reconstruir desde ahí.
- [[Falsación]] — buscar activamente cómo refutar una explicación.
- [[Pensamiento Bayesiano]] — actualización incremental de creencias proporcional a la evidencia.
- [[Abducción]] — inferir la explicación más plausible ante una observación.
- [[Analogías]] — transferir estructura de un dominio conocido a uno nuevo.
- [[Descomposición]] — dividir un problema complejo en partes manejables.
- [[Modelado]] — construir una representación simplificada pero útil de un fenómeno.
- [[Pensamiento Contrafactual]] — explorar "qué habría pasado si..." para aislar un efecto real.

Ver también: [[Arquitectura Cognitiva del Sistema]] · [[MOC - Cognición]]
