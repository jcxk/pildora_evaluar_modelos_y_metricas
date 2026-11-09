# Guía de estudio: Evaluación de modelos (versión sencilla)

Solo lo crítico, para entender el tema antes de presentarlo. Los números son los de **tu demo** (`demo_metricas_titanic.ipynb`), los mismos que salen en las diapositivas.

---

## 0. Lo mínimo que necesitas saber antes

**¿Qué es un modelo?** Un programa que aprende patrones de ejemplos. Le das 700 pasajeros del Titanic con su respuesta (sobrevivió o no) y aprende cosas como «mujer de 1ª clase → casi seguro sobrevive».

**¿Qué es entrenar?** Enseñarle esos ejemplos. En código, una línea: `modelo.fit(X_train, y_train)`.

**¿Qué es train y test?** Separar los datos en dos montones antes de empezar:

- **Train (80 %):** los apuntes con los que estudia el modelo.
- **Test (20 %):** el examen, con preguntas que **nunca ha visto**.

> Si examinas al modelo con las mismas preguntas que estudió, no sabes si aprendió o si memorizó. Por eso se evalúa siempre con test.

En tu demo: 712 pasajeros para train y **179 para test** (69 sobrevivieron, 110 murieron).

---

## 1. La idea de toda la píldora

> **Evaluar = comparar lo que dijo el modelo con lo que pasó de verdad, en datos que no vio.**

Todo lo demás son formas distintas de contar aciertos y fallos.

---

## 2. La matriz de confusión (lo más importante)

Cruzas lo que dijo el modelo con la realidad y salen 4 casillas:

|  | Dijo: **sobrevive** | Dijo: **muere** |
|---|---|---|
| **De verdad sobrevivió** | **46** ✅ TP | **23** ❌ FN |
| **De verdad murió** | **12** ❌ FP | **98** ✅ TN |

**Truco para no liarte:** se lee de atrás hacia delante.

- La **segunda palabra** es lo que dijo el modelo: Positivo = «sobrevive», Negativo = «muere».
- La **primera palabra** dice si acertó: Verdadero = acertó, Falso = falló.

Ejemplos:

- **Falso Negativo (FN):** dijo «muere» (negativo) y se equivocó (falso). Sobrevivió y lo dio por muerto.
- **Falso Positivo (FP):** dijo «sobrevive» (positivo) y se equivocó. Murió y lo dio por vivo.

Si entiendes esta tabla, entiendes el 80 % de la píldora.

---

## 3. Las 4 métricas, una frase cada una

| Métrica | La pregunta que responde | Cálculo | Resultado |
|---|---|---|---|
| **Accuracy** | ¿Cuántas acierta en total? | (46 + 98) / 179 | **80 %** |
| **Precision** | Cuando dice «sí», ¿me puedo fiar? | 46 / (46 + 12) | **79 %** |
| **Recall** | De todos los «sí» reales, ¿cuántos encuentra? | 46 / (46 + 23) | **67 %** |
| **F1** | Equilibrio entre precision y recall | media de las dos (ver abajo) | **72 %** |

### Precision vs recall: la analogía del pescador

Lanzas una red en un lago:

- **Precision:** de lo que sacas en la red, ¿cuánto es pescado y cuánto basura? (*¿es fiable lo que pesco?*)
- **Recall:** de todos los peces del lago, ¿cuántos has pescado? (*¿se me escapa alguno?*)

Una red enorme pesca todos los peces (recall alto) pero también mucha basura (precision baja). Una red pequeñita solo saca peces (precision alta) pero se le escapan muchos (recall bajo).

### ¿Cuál importa más? Depende de qué error sale más caro

| Caso | Error grave | Métrica a vigilar |
|---|---|---|
| Filtro de spam | Mandar a spam un email importante (FP) | **Precision** |
| Detectar cáncer | Decirle «estás sano» a un enfermo (FN) | **Recall** |
| Detectar fraude | Dejar pasar un fraude (FN) | **Recall** |

### F1 en una línea

Es una media «exigente» de precision y recall: **si una de las dos es mala, el F1 es malo**. No se puede hacer trampa sacando una alta y la otra a cero.

Fórmula, por si te la piden: `2 × P × R / (P + R)`.

---

## 4. La trampa del accuracy

Un modelo **tonto** que dice siempre «muere», sin mirar nada:

- Acierta a los 110 que murieron → 110 / 179 = **61 % de accuracy**.
- No encuentra ni un superviviente → **recall 0 %, F1 0 %**.

> Un 61 % sin haber aprendido nada. Por eso **el accuracy solo, engaña**, sobre todo cuando una clase es mucho más grande que la otra.

Regla práctica: compara siempre tu modelo con el tonto. Tu modelo saca 80 % contra 61 %, así que sí ha aprendido algo.

*(Cómo arreglar el problema de las clases desequilibradas: lo explican en la píldora del 12/11. Tú solo cuentas el problema.)*

---

## 5. El umbral: de dónde salen el «sí» y el «no»

El modelo en realidad no dice «sí» o «no». Dice una **probabilidad**: «este pasajero tiene un 0,73 de sobrevivir».

Luego se aplica un **umbral**, por defecto 0,5: por encima dice «sobrevive» y por debajo, «muere».

Si mueves el umbral, cambian precision y recall. Estos son los resultados reales de tu demo:

| Umbral | Precision | Recall | Qué pasa |
|---|---|---|---|
| 0,2 | 57 % | 84 % | Dice «sí» con poco: encuentra a casi todos, pero con muchas falsas alarmas |
| **0,5** | **79 %** | **67 %** | El equilibrio por defecto |
| 0,8 | 91 % | 30 % | Solo dice «sí» si está segurísimo: fiable, pero se le escapan muchos |

> **Si subes una, baja la otra.** Elegir el umbral es una decisión de negocio, no matemática.

---

## 6. ROC-AUC (solo la idea)

- **Curva ROC:** dibuja cómo se comporta el modelo con **todos los umbrales a la vez**.
- **AUC:** el área bajo esa curva, un solo número para resumirla.

| AUC | Significado |
|---|---|
| 0,5 | Como tirar una moneda |
| > 0,8 | Bueno |
| 1 | Perfecto |

Tu modelo: **AUC = 0,84**, bueno. Sirve sobre todo para **comparar modelos** sin tener que elegir un umbral.

---

## 7. Multiclase (para su proyecto)

Cuando hay más de 2 clases (por ejemplo 1ª, 2ª y 3ª clase del billete):

- La matriz se hace más grande: una fila y una columna por clase.
- **Los aciertos están en la diagonal.**
- Precision, recall y F1 se calculan **para cada clase por separado**.

Para resumir todo en un número, `classification_report` da dos medias:

| Media | Cómo se calcula | Cuidado |
|---|---|---|
| **Macro avg** | Media simple: todas las clases pesan igual | Si una clase va mal, se nota |
| **Weighted avg** | Pesa más la clase con más ejemplos | Puede **esconder** una clase pequeña que va mal |

Consejo: con clases desequilibradas, mira el **macro**.

---

## 8. Regresión: cuando predices un número

Si el modelo predice un número (por ejemplo, el precio del billete), ya no hay aciertos y fallos: hay **errores más grandes o más pequeños**.

| Métrica | Qué significa | En pocas palabras |
|---|---|---|
| **MAE** | Error medio | «De media me equivoco en X libras». La más fácil de explicar |
| **RMSE** | Error medio que castiga más los errores grandes | Si es mucho mayor que el MAE, hay algún error enorme |
| **R²** | Qué parte de la realidad explica el modelo | 1 = perfecto · 0 = igual que predecir siempre la media |

(El **MSE** es el RMSE sin la raíz cuadrada; está en unidades raras, como libras², y por eso se usa poco para explicar resultados.)

---

## 9. Chuleta final

| Situación | Métrica |
|---|---|
| Clases equilibradas, todos los errores pesan igual | Accuracy |
| Un falso positivo sale caro | Precision |
| Un falso negativo sale caro | Recall |
| Clases desequilibradas, o importan los dos errores | F1 |
| Comparar modelos sin elegir umbral | ROC-AUC |
| Varias clases, alguna pequeña | Macro avg |
| Regresión, explicarlo fácil | MAE |
| Regresión, castigar errores grandes | RMSE |

> **La frase que lo resume todo:** no existe la mejor métrica; se elige según qué error es más caro en tu problema.

---

## 10. Preguntas que te pueden hacer (y qué contestar)

**«¿Cuál es la mejor métrica?»**
Ninguna en general. Depende de qué error es más caro en tu problema.

**«¿Por qué no usar solo accuracy?»**
Porque un modelo que no ha aprendido nada puede sacar un accuracy alto si una clase domina (el 61 % del modelo tonto, o el 99 % en fraude).

**«¿Qué diferencia hay entre precision y recall?»**
Precision: cuando dice que sí, ¿acierta? Recall: de todos los que eran sí, ¿cuántos encontró?

**«¿Qué es un buen AUC?»**
Por encima de 0,8 suele ser bueno; 0,5 es azar.

**«¿Por qué se evalúa con test y no con train?»**
Porque el modelo ya ha visto train: sería como hacer el examen con las preguntas que ya estudió.

**Si no sabes la respuesta:** «Buena pregunta, lo miro y os lo paso». Es totalmente válido.

---

## 11. Autotest: comprueba que lo has entendido

<details>
<summary>1. Un pasajero sobrevivió y el modelo dijo «muere». ¿Qué casilla es?</summary>

Falso Negativo (FN): el modelo dijo negativo («muere») y se equivocó.
</details>

<details>
<summary>2. Titanic, «mujeres y niños primero» con 100 pasajeros: TP=30, FN=8, FP=12, TN=50. Calcula accuracy, precision, recall y F1.</summary>

- Accuracy = (30 + 50) / 100 = **80 %**
- Precision = 30 / (30 + 12) ≈ **71 %**
- Recall = 30 / (30 + 8) ≈ **79 %**
- F1 = 2·30 / (2·30 + 12 + 8) = 60 / 80 = **75 %**

Encuentra a casi 8 de cada 10 supervivientes, pero no llega al listón de 0,80 del caso de rescate.
</details>

<details>
<summary>3. Quieres detectar enfermos de cáncer. ¿Qué métrica priorizas?</summary>

Recall: lo peor es que se te escape un enfermo (falso negativo).
</details>

<details>
<summary>4. Si bajas el umbral de 0,5 a 0,2, ¿qué pasa con precision y recall?</summary>

El recall sube (encuentra a más) y la precision baja (más falsas alarmas).
</details>

<details>
<summary>5. En un problema multiclase con una clase muy pequeña que va mal, ¿qué media lo delata mejor, macro o weighted?</summary>

Macro: todas las clases pesan igual, así que la clase pequeña que falla baja la media.
</details>
