# 🎵 Spotify Pop Analyzer: Clasificación de Géneros Musicales mediante Minería de Datos

> **Proyecto final del curso de Minería de Datos de la Univrsidad Tecnologica Metropolitana** 

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=flat-square)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-Classification-orange?style=flat-square)
![Methodology](https://img.shields.io/badge/Methodology-CRISP--DM-green?style=flat-square)
![Status](https://img.shields.io/badge/Status-Completed-success?style=flat-square)

## 📄 Resumen Ejecutivo (Abstract)

Este proyecto aborda la problemática de la clasificación automática de géneros musicales en plataformas de *streaming*, un componente crítico para los sistemas de recomendación modernos. Utilizando la metodología estándar de la industria **CRISP-DM** (Cross-Industry Standard Process for Data Mining), se desarrolló un modelo predictivo capaz de identificar el género "Pop" basándose exclusivamente en **características espectrales y métricas de audio** extraídas de la API de Spotify.

El estudio pone énfasis en la **ingeniería de características robusta** y el tratamiento de datos desbalanceados para mitigar sesgos en la clasificación.

## 🎯 Objetivos y Contexto del Negocio

En el contexto de la musicología computacional y los sistemas de recomendación (RecSys), la clasificación basada en metadatos (artista, álbum) es insuficiente. El objetivo de este estudio es:
1.  **Modelar la "Huella Acústica":** Determinar qué patrones matemáticos (ritmo, energía, valencia) definen al género Pop frente a otros estilos.
2.  **Maximizar Métricas de Recuperación:** Priorizar el *Recall* y la *Precisión* para asegurar que las canciones sugeridas al usuario sean pertinentes.

## 🔬 Ingeniería de Datos y Preprocesamiento Avanzado

La fase de preparación de datos (`Data Preparation` en CRISP-DM) fue la más exhaustiva del proyecto, abordando la ruidosa naturaleza de los datasets de audio.

### 1. Limpieza y Depuración (Data Cleaning)
* **Gestión de Redundancias:** Se implementaron algoritmos para detectar duplicados implícitos basados en IDs de pista (`track_id`), eliminando el sesgo introducido por canciones populares presentes en múltiples listas de reproducción.
* **Reducción de Ruido:** Eliminación de variables de metadatos no predictivos (`track_name`, `video_error`) que aumentaban la dimensionalidad sin aportar ganancia de información.

### 2. Selección de Características (Feature Selection)
Se aplicó un análisis estadístico para filtrar variables, utilizando una **Matriz de Correlación de Pearson** para detectar multicolinealidad:
* **Hallazgo Clave:** Se detectó una fuerte correlación positiva entre `energy` y `loudness`. Se evaluó la eliminación de redundancias para reducir la varianza del modelo.
* **Variables Predictoras Seleccionadas:** `danceability`, `energy`, `valence` (positividad musical), `acousticness`, `instrumentalness`, `tempo` y `speechiness`.

### 3. Transformación y Normalización
Dado que las variables de audio tienen escalas heterogéneas (ej. `tempo` en BPM vs `danceability` en rango 0-1), se aplicaron técnicas de escalado para garantizar la convergencia de los algoritmos basados en gradiente y distancia:
* **Standard Scaler (Z-Score):** Estandarización de variables numéricas para obtener una distribución con $\mu=0$ y $\sigma=1$.
* **Target Encoding:** Transformación de la variable objetivo multiclase (`playlist_genre`) a un problema de clasificación binaria para aislar los patrones del género Pop.

### 4. Manejo de Desbalance de Clases (Class Imbalance)
El dataset original presentaba una distribución desigual entre géneros. Se aplicaron estrategias de muestreo (**Sampling**) en el conjunto de entrenamiento para equilibrar la clase minoritaria y evitar que el modelo converja hacia una solución trivial (predecir siempre la clase mayoritaria).

## 📊 Modelado y Resultados

Se entrenaron y validaron algoritmos de aprendizaje supervisado utilizando `Scikit-Learn`. El análisis de importancia de características (*Feature Importance*) reveló que:
* La **Danceability** (capacidad bailable) y la **Valence** (sentimiento positivo) son los discriminadores más potentes para el Pop.
* El modelo logra generalizar correctamente patrones acústicos, diferenciando el Pop de géneros con alta energía pero baja valencia (como el Rock o el EDM).

## 📂 Estructura del Repositorio

```text
Spotify-Pop-Classification/
│
├── 📓 Pop_Music_Model.ipynb       # Notebook principal: EDA, ETL y Pipeline de Modelado
├── 📂 docs/
│   └── Informe_Final_Mineria.pdf  # Documentación técnica detallada (Fases CRISP-DM)
└── 📄 README.md                   # Presentación del proyecto
```
##🛠️ Stack Tecnológico
Lenguaje: Python 3.x 🐍

Análisis de Datos: Pandas, NumPy.

Visualización Científica: Seaborn, Matplotlib.

Machine Learning: Scikit-Learn (Preprocesamiento, Modelado, Métricas).

👥 Créditos y Autoría
Este proyecto fue desarrollado como parte de la cátedra de Minería de Datos de la carrera de Ingeniería Civil en Computación.

Patricio Abarca - Investigación, Ingeniería de Datos y Modelado - https://github.com/Begluckt
