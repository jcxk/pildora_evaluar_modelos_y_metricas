# AGENTS.md

Contexto del proyecto para agentes de IA (Claude Code, Codex, Cursor, etc.) y para cualquier persona que retome el trabajo. Actualizado: 07/11/2026.

## Qué es este proyecto

Píldora individual **«Evaluación de modelos y métricas de rendimiento»** del módulo M2: Data Analytics & Machine Learning (Factoría F5, P1 IA School BCN).

- **Fecha:** 11/11/2026
- **Formato:** 45 min de explicación (**sin demo en vivo**, decisión del 07/11) + 15 min de Kahoot.
- **Entregable principal:** diapositivas para hablar 45 minutos, no una guía de estudio.
- **Público:** compañeros del bootcamp, nivel principiante. Hasta ahora solo han visto EDA con el Titanic (ver `RESOURCES.md`); no han entrenado modelos ni calculado métricas.

## Rúbrica (ver `SPECS.md`)

4 criterios de 25 puntos cada uno:

1. Un poco de inglés, también hablado.
2. Teoría y práctica, con énfasis en la práctica.
3. Duración mínima de 1 hora.
4. Repositorio en GitHub y/o artículo en Medium.

## Decisiones tomadas (respetarlas)

- **Inglés: SOLO la diapositiva 3 (`contexto`, el proceso completo de 9 pasos)**; en el resto nada en inglés, ni etiquetas de gráficos ni notas, decisión del usuario del 09/11. Unos 5 min hablados en inglés, con el guion en inglés en sus notas. El resto de materiales, en castellano. Los nombres técnicos de las métricas (precision, recall, F1…) se usan tal cual.
- **Kahoot: todas las preguntas en castellano.**
- **Solo explicación, sin parte en vivo.** La práctica se cubre con mini ejercicios en las diapositivas al estilo Código Máquina (celda de Jupyter con import, listas pequeñas y su `Out` real), cálculos a mano y preguntas de cálculo en el Kahoot.
- Todo en castellano, con ejemplos del **Titanic** para conectar con el EDA que ya conocen.
- **Repositorio:** https://github.com/jcxk/pildora_evaluar_modelos_y_metricas (subido el 09/11 a petición del usuario). La carpeta `slides/` (material de Código Máquina) está en `.gitignore`: no se publica.

## Calendarios: qué evitar y a qué hacer referencia

Hay dos calendarios y los dos cuentan:

- **`CALENDAR_TALKS.md`:** las píldoras de los compañeros, una por día.
- **`COURSE_CALENDAR.md`:** las lecciones y proyectos oficiales.

| Fecha | Qué hay | Implicación para la píldora |
|---|---|---|
| 09/11 | Píldora: algoritmos de clasificación | Ya saben qué es un modelo de clasificación |
| 10/11 | Píldora: división de datos · Lección: Modelos de Clasificación · **Inicio del proyecto de clasificación multiclase** (hasta 18/11) | No repetir train/test; «como visteis ayer». Las métricas multiclase les sirven para el proyecto |
| 11/11 | **Esta píldora** · Lecciones: Train test split y Cross validation | No profundizar en split ni en validación cruzada |
| 12/11 | Píldora: datos desbalanceados · Lección: Categorical encoding | Mostrar por qué el accuracy engaña, sin explicar técnicas de balanceo. El encoding de la demo se menciona sin detenerse |
| 17/11 | Píldora: overfitting y regularización · Lección: Sesgo vs varianza | No entrar en overfitting |

## Archivos del repo

| Archivo | Qué es |
|---|---|
| `SPECS.md` | Enunciado, rúbrica, formato y fecha |
| `RESOURCES.md` | Lo que se les ha enseñado hasta ahora (EDA Titanic) |
| `CALENDAR_TALKS.md` | Calendario de píldoras |
| `COURSE_CALENDAR.md` | Calendario oficial del curso |
| `demo_metricas_titanic.ipynb` | Notebook con el Titanic completo. Ya no se usa en vivo; de él salen los números reales (46/23/12/98) |
| `presentacion/` | La presentación en HTML (reveal.js) |
| `slides/` | (Solo local, no se sube) Capturas y transcripciones de dos vídeos de Código Máquina (métricas de clasificación y de regresión), la referencia de estilo |
| `GUIA_ESTUDIO.md` | Guía de estudio sencilla («para tontos»), solo conceptos críticos, con los números reales de la demo. Para que el ponente entienda el tema (no es el entregable) |

## Diapositivas

- **Presentación: `presentacion/index.html` (reveal.js 5.1.0 por CDN), la fuente de verdad desde el 09/11.** Elementos que aparecen al pulsar: `class="fragment"` + `data-fragment-index`. Notas: `<aside class="notes">` (tecla S). Imágenes en `presentacion/img/`.
- Versión anterior (ya no se mantiene): https://claude.ai/artifact/EJB1fz5wqSDNtCvaRV2Aa6, de la que se convirtió.
- 32 diapositivas con notas del presentador (qué decir, tiempos, preguntas al público).
- Agenda: contexto (proceso completo de 9 pasos) 4 min → clasificación 20 → regresión 6 → elegir métrica 3 → **caso Titanic 9** → cierre 3 → Kahoot 15.
- **Caso Titanic** (9 diapositivas `caso-*`, solo escenificado, sin código en vivo). Objetivo de rescate: recall ≥ 0,80 y precision ≥ 0,60. Candidatos con resultados reales en los 179 de test (calculados el 07/11, mismo split):
  - «Todos mueren»: acc 0,61 · recall 0 → suspende
  - Regla del EDA «mujer → sobrevive» (sin entrenar): acc 0,78 · P 0,74 · R 0,65 (TP45 FN24 FP16 TN94) → suspende
  - Regresión logística (umbral 0,5): acc 0,80 · P 0,79 · R 0,67 · AUC 0,84 → suspende
  - Árbol de decisión (`random_state=42`, sin límite): train 0,98 / test 0,82 · P 0,78 · R 0,74 (TP51 FN18 FP14 TN96) · AUC 0,81 → suspende y sobreajustado
  - Logística con umbral 0,25: acc 0,74 · P 0,63 · R 0,81 (TP56 FN13 FP33 TN77) → aprueba. Moraleja: el elegido tiene el peor accuracy (salvo el tonto).
- Las diapositivas de métricas imitan una hoja de Jupyter: título morado, leyenda y/ŷ, fórmula, celda con import + mini ejercicio + `Out`, y a la derecha la cuenta «a mano» y el resultado con el Titanic completo.
- Mini ejercicio de clasificación: `y_verdadero = [0,0,0,0,0,0,1,1,1,1]`, `y_predicho = [0,0,0,0,0,1,1,1,0,0]` → matriz [[5,1],[2,2]], accuracy 0.7, precision 0.667, recall 0.5, F1 0.571.
- Mini ejercicio de regresión: real `[10,30,80]`, predicho `[15,25,60]` → MAE 10, MSE 150, RMSE 12.25 (`root_mean_squared_error`), R² 0.83.
- La diapositiva de la matriz de confusión y la tarjeta «Con el Titanic completo» usan los números reales del notebook (46/23/12/98).
- La diapositiva de multiclase usa una matriz 3×3 de ejemplo inventada (clase del billete), pensada para su proyecto multiclase. Se muestra como imagen real de `ConfusionMatrixDisplay` y con las fórmulas de macro (R₁+R₂+R₃)/3 = 0,77 y weighted (37·R₁+34·R₂+108·R₃)/179 = 0,83.
- **Fórmulas** (decisión del 09/11): en todas las diapositivas de métricas, de la matriz en adelante, como fracción apilada (estilo del Colab de referencia) con la cuenta del mini ejercicio al lado. Colores fijos: FP en naranja (#D84315) y FN en azul (#1565C0). Precision mira los FP, recall los FN y F1 los dos. La chuleta tiene una columna con todas las fórmulas.
- **Imágenes de scikit-learn** (`ConfusionMatrixDisplay.from_predictions`, guía: Colab «Tutorial matriz de confusión y métricas» que pasó el usuario): la diapositiva `matriz-grafica` (unida con la antigua `matriz-codigo`: una celda con `confusion_matrix` + `ConfusionMatrixDisplay` y su `Out`, y el Titanic completo 98/12/23/46) y la de multiclase. Ejes en castellano con `disp.ax_.set(xlabel="Valor predicho", ylabel="Valor verdadero")`. Generadas con `make_cm.py` en el scratchpad y subidas como assets del artifact.
- Las diapositivas de la matriz (`matriz`, `matriz-grafica`) dicen explícitamente que es **clasificación binaria** (2 clases: sobrevive/muere).
- La matriz de la diapositiva 5 (`matriz`) está en el **orden de scikit-learn** `[[TN, FP], [FN, TP]]` (primero 0 = muere), igual que la imagen de la 6, para no confundir. Otras matrices (ejercicio guiado, candidatos del caso) siguen con TP arriba a la izquierda.
- Ejercicio guiado (diapositiva `ejercicio`, siempre con el Titanic, sin COVID): «mujeres y niños primero» con 100 pasajeros, TP30 FN8 FP12 TN50 → accuracy 0,80 · precision 0,71 · recall 0,79 · F1 0,75. Recall justo por debajo del 0,80 del caso. En modo Presentar se revela en 9 pulsaciones: fórmula 1 → resultado 1 → … → resultado 4 → respuesta final. Las fórmulas llevan el número de cada casilla entre paréntesis, p. ej. TP (30) / [TP (30) + FP (12)].
- Ponente en la portada: Juan Carlos E.
- Pendiente de rellenar: el PIN en la diapositiva del Kahoot.

## Notebook (`demo_metricas_titanic.ipynb`)

- Datos: Titanic desde `https://raw.githubusercontent.com/datasciencedojo/datasets/master/titanic.csv` (mismo dataset que el EDA, 891 × 12). Necesita internet.
- Dependencias: pandas, scikit-learn, matplotlib.
- Probado entero sin errores el 05/11/2026. Resultados reales (test de 179 pasajeros, `random_state=42`, `stratify=y`):
  - Matriz: TP=46, FN=23, FP=12, TN=98
  - Accuracy 0,80 · Precision 0,79 · Recall 0,67 · F1 0,72 · AUC 0,84
  - Modelo tonto (DummyClassifier): accuracy 0,61, recall 0, F1 0
- Las diapositivas usan estos mismos números. `GUIA_ESTUDIO.md` también.

## Pendiente

- [ ] Preparar las preguntas del Kahoot (en castellano, varias de cálculo).
- [ ] Decidir dónde va el inglés (lo decide el usuario).
- [x] Repositorio en GitHub con README.
- [ ] Opcional: artículo en Medium.
