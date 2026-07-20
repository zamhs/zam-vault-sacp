---
id: "20260719031101"
tipo: moc
estado: vigente
tags: [moc]
relacionado_con: ["[[Índice]]", "[[Arquitectura Cognitiva del Sistema]]", "[[Epistemología del Sistema]]"]
padre: "[[Índice]]"
---

# MOC - Modelos

Esta carpeta (`/Modelos/`) contiene el conocimiento de **Nivel 2**: síntesis de varias piezas de Nivel 1 (Conceptos, Patrones, Hipótesis, Investigaciones) en explicaciones coherentes de un dominio, con poder explicativo y predictivo. Ver [[Arquitectura Cognitiva del Sistema]] §3 y [[Epistemología del Sistema]] §3-§6 para las reglas exactas de cuándo una Hipótesis se promueve a Modelo, cuándo un Modelo debe revisarse, y cómo se gestionan sus contradicciones.

Un Modelo vive en uno de cuatro estados: `incipiente`, `consolidado`, `en_revision`, `obsoleto`. Usa `Sistema/Plantillas/Plantilla - Modelo.md` para crear notas nuevas.

El conjunto de todos los Modelos, conectados entre sí y con el resto de la Memoria, es lo que da lugar al **Modelo del Mundo** (Nivel 3) — que no tiene carpeta ni nota propia porque es una comprensión emergente, no un objeto estático. Ver [[Índice]] para su explicación completa.

## Listado (activable con Dataview)

```text
FROM "Modelos"
WHERE estado != "obsoleto"
SORT confianza DESC
```

## Notas

*(pendiente de poblar — carpeta vacía al momento de creación del vault)*

## Ver también

[[Índice]] · [[Arquitectura Cognitiva del Sistema]] · [[Epistemología del Sistema]] · [[MOC - Hipótesis]]
