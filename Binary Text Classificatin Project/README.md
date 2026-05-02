# 🎬 Binary Text Classification — IMDB Sentiment Analysis

Clasificación binaria de reseñas de películas (positiva / negativa) usando técnicas de NLP y múltiples algoritmos de Machine Learning con **scikit-learn**.

---

## 📋 Descripción

Este proyecto entrena y evalúa varios modelos de clasificación sobre el dataset público de reseñas de IMDB. Se comparan cuatro algoritmos distintos y se aplica ajuste de hiperparámetros mediante búsqueda en rejilla.

---

## 📁 Estructura del proyecto

```
├── Sklearn Tutorial (Binary Text Classification).ipynb
├── IMDB Dataset.csv
└── README.md
```

---

## 🗃️ Dataset

- **Fuente:** [IMDB Dataset of 50K Movie Reviews](https://www.kaggle.com/datasets/lakshmi25npathi/imdb-dataset-of-50k-movie-reviews)
- **Columnas:** `review` (texto), `sentiment` (`positive` / `negative`)
- **Muestras utilizadas:** 9 000 positivas + 1 000 negativas → balanceadas con `RandomUnderSampler` → **2 000 muestras balanceadas**

---

## ⚙️ Pipeline

```
Dataset IMDB
    │
    ├─ Selección de muestra (9 000 pos + 1 000 neg)
    ├─ Balanceo con RandomUnderSampler
    ├─ Split train/test (67% / 33%)
    ├─ Vectorización con TF-IDF (stop_words='english')
    │
    ├─ Entrenamiento
    │     ├─ Support Vector Machine (SVC lineal)
    │     ├─ Decision Tree
    │     ├─ Naive Bayes (Gaussian)
    │     └─ Logistic Regression
    │
    └─ Evaluación
          ├─ Accuracy
          ├─ F1-Score
          ├─ Classification Report
          ├─ Confusion Matrix
          └─ GridSearchCV (optimización de SVC)
```

---

## 📊 Resultados

| Modelo | Accuracy |
|---|---|
| **SVM (kernel lineal)** | **83.0%** |
| Logistic Regression | 82.0% |
| Decision Tree | 68.2% |
| Naive Bayes | 63.8% |

### Mejor modelo — SVM (kernel lineal)

```
              precision    recall  f1-score   support

    positive       0.83      0.84      0.83       335
    negative       0.83      0.82      0.83       325

    accuracy                           0.83       660
   macro avg       0.83      0.83      0.83       660
weighted avg       0.83      0.83      0.83       660
```

### GridSearchCV — Optimización de SVC

```python
Mejores parámetros: {'C': 1, 'kernel': 'rbf'}
Mejor score CV:      83.06%
```

---

## 🛠️ Tecnologías

- Python 3.x
- [scikit-learn](https://scikit-learn.org/)
- [imbalanced-learn](https://imbalanced-learn.org/)
- pandas / NumPy
- Google Colab

---

## 🚀 Cómo ejecutar

1. Clona el repositorio:
   ```bash
   git clone https://github.com/tu-usuario/tu-repositorio.git
   cd tu-repositorio
   ```

2. Instala las dependencias:
   ```bash
   pip install scikit-learn imbalanced-learn pandas numpy
   ```

3. Descarga el dataset de Kaggle y colócalo en la raíz del proyecto como `IMDB Dataset.csv`.

4. Abre el notebook en Google Colab o Jupyter y ejecuta las celdas en orden.

---

## 💡 Conceptos clave

- **CountVectorizer** — cuenta la frecuencia de cada palabra en el corpus.
- **TF-IDF** — pondera la relevancia de una palabra: alta frecuencia local + baja frecuencia global.
- **RandomUnderSampler** — equilibra clases mayoritaria y minoritaria eliminando muestras.
- **GridSearchCV** — búsqueda exhaustiva de hiperparámetros con validación cruzada.

---

## 📄 Licencia

Este proyecto se distribuye bajo la licencia MIT.
