# MODELO DE MACHINE LEARNING PARA PREDECIR LA DESERCION DE CLIENTES

## Descripción General

Este proyecto tiene como objetivo desarrollar modelos de Machine Learning para predecir el 'Churn' (abandono de clientes) en la empresa de telecomunicaciones TELECOM X. La predicción proactiva del churn permite a la empresa identificar a los clientes en riesgo y aplicar estrategias de retención dirigidas, lo que es fundamental para optimizar los recursos y mejorar la rentabilidad.

## Contenido del Notebook

El análisis se estructura en las siguientes fases:

1.  **Importación de Librerías y Datos:** Carga de las librerías necesarias (pandas, numpy, matplotlib, seaborn, sklearn) y del conjunto de datos `df_normalized.xlsx`.

2.  **Análisis y Limpieza de Datos:**
    *   Verificación y manejo de valores faltantes (eliminación de filas con `Churn` nulo).
    *   Confirmación de la ausencia de `customerID` duplicados.
    *   Eliminación de la columna `customerID` por ser irrelevante para el modelado.
    *   **Corrección crucial:** Conversión de la columna `Charges.Total` a tipo numérico, ya que inicialmente se detectó como 'object' y esto afectaba la codificación.

3.  **Análisis Exploratorio de Datos (EDA):**
    *   Visualización de la distribución del Churn.
    *   Exploración de la relación entre `Churn` y variables clave como `tenure` (antigüedad), `gender` (género), `Contract` (tipo de contrato) y `Charges.Total` (cargos totales).

4.  **Codificación de Variables Categóricas:**
    *   Aplicación de One-Hot Encoding (`pd.get_dummies`) a las variables categóricas identificadas (`gender`, `Partner`, `Dependents`, `PhoneService`, `MultipleLines`, `InternetService`, `OnlineSecurity`, `OnlineBackup`, `DeviceProtection`, `TechSupport`, `StreamingTV`, `StreamingMovies`, `Contract`, `PaperlessBilling`, `PaymentMethod`, `Churn`). Esto transforma las categorías en un formato numérico (0 y 1) adecuado para los algoritmos de Machine Learning, evitando el error de codificar variables numéricas continuas como `Charges.Total`.

5.  **Preparación de Datos para el Modelado:**
    *   Definición de las características (`X`) y la variable objetivo (`y`, que es `Churn_Yes`).
    *   División del conjunto de datos en un 70% para entrenamiento y un 30% para prueba, utilizando `stratify=y` para mantener la proporción de la clase `Churn` en ambos conjuntos.

6.  **Modelado Predictivo:**
    *   **Árbol de Decisión (`DecisionTreeClassifier`):** Entrenamiento de un modelo de árbol de decisión.
    *   **Random Forest (`RandomForestClassifier`):** Entrenamiento de un modelo Random Forest (ensamble de árboles de decisión).

7.  **Evaluación de Modelos:**
    *   Cálculo y visualización de métricas clave para ambos modelos en el conjunto de prueba:
        *   Accuracy
        *   Precision
        *   Recall
        *   F1-Score
    *   Generación de **Matrices de Confusión** para entender los Verdaderos Positivos, Verdaderos Negativos, Falsos Positivos y Falsos Negativos de cada modelo.
    *   Comparación visual de las distribuciones de Churn Real vs. Predicciones de ambos modelos.

## Resultados Clave del Modelado

### Métricas de Evaluación:

| Modelo            | Accuracy | Precision | Recall | F1-Score |
| :---------------- | :------- | :-------- | :----- | :------- |
| Árbol de Decisión | 0.7198   | 0.4743    | 0.5098 | 0.4914   |
| Random Forest     | 0.7586   | 0.5541    | 0.4652 | 0.5058   |

### Análisis de los Modelos:

*   El **Random Forest** se posiciona como el modelo más robusto, superando al Árbol de Decisión en **Accuracy, Precision y F1-Score**. Esto indica que tiene un mejor rendimiento general y es más preciso en sus predicciones de churn.
*   Aunque el **Árbol de Decisión** mostró un `Recall` marginalmente más alto (0.5098 vs 0.4652), el **Random Forest** ofrece un balance más adecuado entre la identificación de clientes que se van y la certeza de que esas predicciones son correctas.

## Conclusiones Orientadas al Negocio

Este análisis proporciona a TELECOM X una herramienta predictiva valiosa para la gestión del churn, permitiendo una estrategia proactiva en lugar de reactiva:

1.  **Identificación Proactiva de Clientes en Riesgo:** El modelo Random Forest puede ser implementado para identificar a los clientes con mayor probabilidad de abandonar la empresa, incluso antes de que muestren signos evidentes de insatisfacción.

2.  **Optimización de Campañas de Retención:** Con una precisión del 55.41%, el Random Forest permite a TELECOM X dirigir sus recursos de retención de manera más eficiente. Más de la mitad de las veces que el modelo predice un churn, acertará, lo que reduce el gasto en clientes que no tenían intención de irse.

3.  **Foco en la Retención y Rentabilidad:** Al predecir el churn con mayor confiabilidad, TELECOM X puede diseñar e implementar estrategias de retención personalizadas (ofertas, mejoras de servicio, soporte proactivo) para los clientes identificados, lo que es significativamente más rentable que la adquisición de nuevos clientes.

4.  **Información para Decisiones Estratégicas:** Los factores que más influyen en el churn (que se pueden derivar de la importancia de las características del Random Forest) pueden guiar a la empresa en la mejora de sus productos, servicios y políticas de contrato para reducir el churn a largo plazo.

En resumen, el modelo Random Forest desarrollado en este proyecto es una herramienta estratégica que TELECOM X puede utilizar para mejorar la satisfacción del cliente, optimizar sus operaciones y fortalecer su posición en el mercado mediante una gestión de churn más inteligente y eficiente.

