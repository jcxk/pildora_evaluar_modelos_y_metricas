# Evaluación de modelos y métricas de rendimiento

Píldora del módulo M2 · Data Analytics & Machine Learning (Factoría F5, P1 IA School BCN) · 11/11/2026 · Juan Carlos E.

45 minutos de explicación con ejemplos del **Titanic** y 15 minutos de Kahoot.

## Presentación

**En línea:** https://jcxk.github.io/pildora_evaluar_modelos_y_metricas/

En local: abre [`presentacion/index.html`](presentacion/index.html) en el navegador (necesita internet para las fuentes y reveal.js).

| Tecla | Qué hace |
|---|---|
| Espacio / → | Siguiente paso o diapositiva |
| S | Vista del ponente con las notas |
| F | Pantalla completa |
| Esc | Vista general de todas las diapositivas |

Cada diapositiva es un `<section>` de 1920×1080 dentro de `presentacion/index.html`. Para que algo aparezca al pulsar, añádele `class="fragment"` y `data-fragment-index="N"` (el orden). Las notas del ponente van en `<aside class="notes">`.

## Contenido

1. Contexto: el proceso completo de machine learning (en inglés).
2. Clasificación binaria: matriz de confusión (en el orden de scikit-learn), accuracy, precision, recall, F1, ROC-AUC y multiclase, cada una con su fórmula y un mini ejercicio en celda de Jupyter.
3. Regresión: MAE, MSE, RMSE y R².
4. Caso práctico: cuatro modelos del Titanic juzgados con métricas, de principio a fin.

## Archivos

| Archivo | Qué es |
|---|---|
| `presentacion/` | La presentación (reveal.js) y las imágenes de `ConfusionMatrixDisplay` |
| `demo_metricas_titanic.ipynb` | Notebook con el Titanic completo del que salen los números reales |
| `GUIA_ESTUDIO.md` | Guía de estudio sencilla de los conceptos |
| `AGENTS.md` | Contexto y decisiones del proyecto |
| `SPECS.md`, `RESOURCES.md`, `*_CALENDAR*.md` | Enunciado, recursos y calendarios del curso |
