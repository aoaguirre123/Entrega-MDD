# Análisis y Predicción de Precios de Autos Usados

Este proyecto fue desarrollado como parte de la **2° Evaluación de la asignatura de Minería de Datos**. El objetivo principal es analizar un conjunto de datos del mercado automotriz (Kaggle) y construir modelos analíticos capaces de predecir de forma precisa el precio de venta de vehículos usados en función de sus características mecánicas y comerciales.

**Integrantes del equipo:**
* Víctor Yáñez
* Aoris Aguirre

---

## Descripción del Dataset

El conjunto de datos original cuenta con **2,000 registros** y contempla variables tanto cuantitativas como cualitativas. Tras el análisis exploratorio de datos (EDA), las variables con mayor impacto directo sobre la variable objetivo (`Price`) fueron:
* **Engine_Size (Tamaño del motor):** Correlación positiva fuerte (0.61).
* **Horsepower (Caballos de fuerza):** Correlación positiva moderada-alta (0.51).
* **Model_Year (Año del vehículo):** Correlación positiva moderada (0.47).
* **Mileage (Kilometraje):** Correlación negativa (-0.27), indicando que a menor recorrido, mayor valor.

---

## Preprocesamiento y Justificación Técnica

Dado que la variable objetivo (`Price`) es numérica y continua, el problema se abordó desde el enfoque del **Aprendizaje Supervisado de Regresión**.

Para permitir que los algoritmos procesaran de forma correcta las variables cualitativas (`Brand`, `Fuel_Type` y `Transmission`), se aplicó una transformación de **One-Hot Encoding**, expandiendo el conjunto de datos original a una matriz puramente numérica denominada `df_final`. Posteriormente, los datos se dividieron en una proporción estándar de **80% para entrenamiento** y **20% para pruebas**.

---

## Modelos Implementados y Resultados

Para evaluar el comportamiento del mercado, se entrenaron y contrastaron dos enfoques matemáticos distintos:

1. **Regresión Lineal Múltiple (Modelo Base):** Asume que las características aportan o restan valor de manera proporcional y recta.
2. **Árbol de Decisión Regressor:** Construye un esquema de reglas lógicas sucesivas para capturar comportamientos no lineales (configurado con una profundidad máxima de 5 para evitar sobreajuste).

### Cuadro Comparativo de Rendimiento

| Métrica de Evaluación | Regresión Lineal Múltiple | Árbol de Decisión |
| :--- | :---: | :---: |
| **R² (Capacidad de Ajuste)** | **0.9665** | 0.7295 |
| **MAE (Error Promedio)** | **1442.39** | 3779.12 |

**Conclusión del modelamiento:** La **Regresión Lineal Múltiple es la clara ganadora**. Su impresionante R² de 96.65% demuestra que el dataset cuenta con una estructura fuertemente lineal, superando por completo la rigidez del árbol de decisión y reduciendo el margen de error promedio a menos de la mitad.

---

## Experiencia Práctica y Crítica Constructiva

* **Limitación de los Datos:** El volumen del dataset (2,000 filas) representa un escenario de laboratorio altamente optimizado (Kaggle). 
* **Brecha con la Realidad:** En un entorno comercial real, los precios de los autos usados son más caóticos e influenciados por factores reputacionales de la marca, estados estéticos e historiales de choques que este volumen de información no alcanza a modelar en su totalidad.
* **Solución Propuesta:** Para escalar este proyecto a un nivel profesional o de producción, la solución técnica requiere enriquecer el dataset aumentando el tamaño de la muestra e integrando el historial de mantenciones físicas del vehículo.

---

## Cómo Ejecutar el Proyecto

1. Clonar este repositorio.
2. Asegurarse de contar con las librerías necesarias de Python: `pandas`, `numpy`, `scikit-learn`, `seaborn` y `matplotlib`.
3. Abrir el archivo `.ipynb` directamente en **Google Colab** o Jupyter Notebook.
4. Ejecutar de forma secuencial las celdas de preprocesamiento, visualización y los bloques independientes de modelamiento.
