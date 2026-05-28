# Análisis y Predicción de Precios de Autos Usados

Este proyecto fue desarrollado como parte de la **2° Evaluación de la asignatura de Minería de Datos**. El objetivo principal es analizar un conjunto de datos del mercado automotriz y construir modelos analíticos capaces de predecir de forma precisa el precio de venta de vehículos usados en función de sus características mecánicas y comerciales.

**Integrantes del equipo:**
* Víctor Yáñez
* Aoris Aguirre

---

## Descripción del Dataset

El conjunto de datos utilizado proviene de Kaggle: **[Car Price Prediction and Vehicle Specifications](https://www.kaggle.com/datasets/ihasan88/car-price-prediction-and-vehicle-specifications)**. 

Este dataset recopila especificaciones técnicas y comerciales globales de **2,000 vehículos** pertenecientes a marcas líderes del mercado masivo y de alta gama: *BMW, Ford, Honda, Hyundai, Tesla y Toyota*. 

Tras el análisis exploratorio de datos (EDA), las variables cuantitativas con mayor impacto directo sobre la variable objetivo (`Price`) fueron:
* **Engine_Size (Tamaño del motor):** Correlación positiva fuerte (0.61). Autos con motores más grandes tienden a ser significativamente más caros.
* **Horsepower (Caballos de fuerza):** Correlación positiva moderada-alta (0.51). A mayor potencia, el precio se incrementa de forma constante.
* **Model_Year (Año del vehículo):** Correlación positiva moderada (0.47). Los vehículos más nuevos retienen un mayor valor comercial.
* **Mileage (Kilometraje):** Correlación negativa (-0.27). Muestra un comportamiento lógico de mercado donde a menor recorrido, mayor es el precio.

---

## Preprocesamiento y Justificación Técnica

Dado que la variable objetivo (`Price`) es numérica y continua, el problema se abordó bajo el enfoque del **Aprendizaje Supervisado de Regresión**.

Para permitir que los algoritmos procesaran correctamente la información cualitativa (`Brand`, `Fuel_Type` y `Transmission`), se aplicó una transformación de **One-Hot Encoding**, expandiendo el conjunto de datos original a una matriz puramente numérica denominada `df_final`. Posteriormente, los datos se dividieron de forma aleatoria en una proporción estándar de **80% para entrenamiento** (`X_train`, `y_train`) y **20% para pruebas** (`X_test`, `y_test`).

---

## Modelos Implementados y Resultados

Para evaluar el comportamiento del mercado automotriz en este dataset, se entrenaron y contrastaron dos enfoques matemáticos con filosofías distintas:

1. **Regresión Lineal Múltiple (Modelo Base):** Asume una estructura lineal pura, donde cada característica (potencia, año, kilometraje) aporta o resta valor de manera directamente proporcional y constante a través de una suma ponderada.
2. **Árbol de Decisión Regressor:** Construye un esquema de reglas lógicas sucesivas por ramas (no lineales) para segmentar el mercado automotriz. Se configuró con una profundidad máxima de 5 (`max_depth=5`) para prevenir el sobreajuste.

### Cuadro Comparativo de Rendimiento

| Métrica de Evaluación | Regresión Lineal Múltiple | Árbol de Decisión |
| :--- | :---: | :---: |
| **R² (Capacidad de Ajuste)** | **0.9665** | 0.7295 |
| **MAE (Error Promedio)** | **1442.39** | 3779.12 |

**Conclusión del modelamiento:** La **Regresión Lineal Múltiple es la clara ganadora**. Su impresionante ajuste de 96.65% demuestra que el precio de los automóviles en este conjunto de datos sigue una tendencia recta y predecible. Al verse obligado a limitar su profundidad para no memorizar los datos, el Árbol de Decisión se volvió demasiado rígido (*underfitting*), duplicando ampliamente el margen de error promedio del modelo lineal.

---

## Experiencia Práctica y Crítica Constructiva

* **Análisis del Origen:** Un coeficiente de determinación ($R^2$) de casi el 97% representa un **escenario idealizado o de laboratorio académico**. Al investigar el origen del dataset en Kaggle, confirmamos que las variables cuantitativas han sido fuertemente curadas o calibradas matemáticamente de manera previa por el autor.
* **Brecha con la Realidad:** En el mercado real de autos usados (como portales nacionales o automotoras físicas), el comportamiento de los precios es mucho más caótico. Influyen factores altamente subjetivos y cualitativos como el historial de choques previos, el estado estético interior/exterior, la urgencia de venta y, por sobre todo, el peso reputacional de la marca (un auto de lujo se deprecia de manera drásticamente diferente a uno comercial ante las mismas especificaciones mecánicas). 
* **Solución Propuesta:** Para escalar este modelo de analítica a un entorno profesional o de producción real, la solución técnica requiere enriquecer el dataset aumentando drásticamente la muestra e integrando variables del historial de mantenimientos físicos de los vehículos.

---

## Cómo Ejecutar el Proyecto

1. Clonar este repositorio.
2. Asegurarse de contar con las librerías base de Python: `pandas`, `numpy`, `scikit-learn`, `seaborn` y `matplotlib`.
3. Abrir el archivo `.ipynb` directamente en **Google Colab** o Jupyter Notebook.
4. Ejecutar de forma secuencial las celdas de carga de datos, análisis exploratorio, binarización y, finalmente, las celdas independientes de modelamiento estadístico.
