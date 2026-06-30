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
* **Mileage (Kilometraje):** Correlación inversa esperada respecto al uso del vehículo.

---

## Metodología Aplicada y Modelos Desarrollados

El pipeline del proyecto combinó aprendizaje no supervisado para segmentación de mercado y aprendizaje supervisado para el modelado predictivo del valor monetario.

### 1. Segmentación de Mercado (K-Means Clustering)
A través de la librería scikit-learn, se aplicó el algoritmo K-Means para segmentar de manera automática el inventario en 3 grupos (clústeres) analizando las especificaciones físicas y el nivel de uso:

* **Clúster 1 (Alto Desgaste / Económico):** Es el segmento más grande del inventario (casi 1,000 vehículos). Agrupa automóviles con el kilometraje promedio más alto (100,867 km) y menor potencia media (215 HP), explicando por qué posee el precio promedio más bajo ($44,417).
* **Clúster 0 (Gama Media / Conservado):** El grupo más pequeño en volumen de unidades. Aunque comparte el año de fabricación (2014) con el Clúster 1, se destaca comercialmente por tener el menor desgaste promedio de la muestra (92,518 km), sosteniendo un precio promedio superior ($45,184).
* **Clúster 2 (Gama Alta / Premium):** El segmento más rentable del negocio. Concentra los vehículos más nuevos (promedio 2016), con motores más potentes (3.06L) y el precio promedio más alto del dataset ($51,341).

---

### 2. Modelado de Regresión (Predicción de Precios)
Se entrenaron y contrastaron tres arquitecturas algorítmicas diferentes en el set de pruebas utilizando un enfoque de validación cruzada estructurado. Los resultados métricos de rendimiento y dispersión de error en la consola fueron los siguientes:

* **Modelo 1: Regresión Lineal Múltiple**
  * **R² (Capacidad de Ajuste):** 0.9665 -> Explica el 96.65% de la variabilidad de los precios.
  * **MAE (Error Absoluto Medio):** $1,442.31 -> Desviación promedio absoluta baja por predicción.
  * **MSE (Error Cuadrático Medio):** 2,766,184.59 -> Demuestra un ajuste sobresaliente y estabilidad ante residuos grandes.
  * **RMSE (Raíz del Error Cuadrático):** $1,663.19 -> Desviación estándar controlada del error típico.

* **Modelo 2: Árbol de Decisión (max_depth=5)**
  * **R² (Capacidad de Ajuste):** 0.7295 -> Explica únicamente el 72.95% de los datos.
  * **MAE (Error Absoluto Medio):** $3,779.12 -> El margen de error promedio se duplica frente a la regresión lineal.
  * **MSE (Error Cuadrático Medio):** 22,323,226.44 -> Denota alta dispersión por predicciones rígidas.
  * **RMSE (Raíz del Error Cuadrático):** $4,724.75 -> Castigo de error típico elevado debido a la naturaleza escalonada de sus divisiones.

* **Modelo 3: Random Forest Regressor (n_estimators=100)**
  * **R² (Capacidad de Ajuste):** 0.9119 -> Explica el 91.19% de la variabilidad.
  * **MAE (Error Absoluto Medio):** $2,172.94 -> Buen balance absoluto promediando sus árboles.
  * **MSE (Error Cuadrático Medio):** 7,270,618.45 -> Penalización matemática controlada ante valores atípicos.
  * **RMSE (Raíz del Error Cuadrático):** $2,696.41 -> Error típico moderado, posicionándose como la segunda mejor alternativa.

---

## Cuadro Comparativo de Resultados

El cuadro resumen confirma que la Regresión Lineal Múltiple es la clara ganadora de este proyecto:

| Métrica de Evaluación | Regresión Múltiple | Árbol de Decisión | Random Forest |
| :--- | :---: | :---: | :---: |
| **R² (Capacidad de Ajuste)** | **0.9665** | 0.7295 | 0.9119 |
| **MAE (Error Absoluto Medio)** | **$1,442.31** | $3,779.12 | $2,172.94 |
| **MSE (Error Cuadrático Medio)** | **2,766,184.59** | 22,323,226.44 | 7,270,618.45 |
| **RMSE (Raíz Error Cuadrático)** | **$1,663.19** | $4,724.75 | $2,696.41 |

### Conclusión General
El comportamiento del precio en este mercado de vehículos es altamente lineal. Aunque implementamos técnicas avanzadas como la segmentación por clústeres (K-Means) y algoritmos basados en ensambles complejos de árboles (Random Forest), la estructura recta de la Regresión Lineal Múltiple demostró ser la arquitectura óptima, más robusta y eficiente para la naturaleza de este negocio automotriz.

---

## Análisis Crítico sobre la Factibilidad Real del Modelo

Es fundamental destacar desde una perspectiva analítica que un coeficente de determinación ($R^2$) de casi el 97% representa un **escenario idealizado o de laboratorio académico**. Al investigar el origen del dataset en Kaggle, confirmamos que las variables cuantitativas han sido fuertemente curadas o calibradas matemáticamente de manera previa por el autor.

* **Brecha con la Realidad:** En el mercado real de autos usados (como portales nacionales o automotoras físicas), el comportamiento de los precios es mucho más caótico. Influyen factores altamente subjetivos y cualitativos como el historial de choques previos, el estado estético interior/exterior, la urgencia de venta y, por sobre todo, el peso reputacional de la marca (un auto de lujo se deprecia de manera drásticamente diferente a uno comercial ante las mismas especificaciones mecánicas). 
* **Solución Propuesta:** Para escalar este modelo de analítica a un entorno profesional o de producción real, la solución técnica requiere enriquecer el dataset aumentando drásticamente la muestra e integrando variables del
