---
title: "Entrada 04 — Práctica 4: Regresion Lineal y Regresion Logistica"
date: 2025-08-19
---

# Entrada 04 — Práctica 4: Regresion Lineal y Regresion Logistica

## Contexto
Actividad de implementación y comparación de modelos de regresión lineal para predicción de valores continuos y regresión logística para problemas de clasificación binaria.

## Objetivos
- Desarrollar un modelo de regresión lineal para predecir precios de viviendas
- Implementar un modelo de regresión logística para diagnóstico médico
- Evaluar el rendimiento de ambos modelos con métricas específicas
- Comparar las diferencias entre problemas de regresión y clasificación

## Actividades (con tiempos estimados)
1. Configuración del entorno y carga de librerías — 10 min
2. Análisis exploratorio del dataset de viviendas — 15 min
3. Entrenamiento y evaluación de regresión lineal — 25 min
4. Análisis del dataset de diagnóstico médico — 15 min
5. Entrenamiento y evaluación de regresión logística — 25 min
6. Comparación y reflexión final — 10 min

## Desarrollo
La práctica 4 se centró en la implementación de dos tipos fundamentales de modelos de machine learning. Para la regresión lineal, se trabajó con el dataset de precios de viviendas de Boston, mientras que para la regresión logística se utilizó el dataset de diagnóstico de cáncer de mama de sklearn.

En la parte de regresión lineal:
- Se identificaron y manejaron valores faltantes usando SimpleImputer con estrategia de mediana
- Se dividieron los datos en conjuntos de entrenamiento y prueba (80/20)
- Se entrenó el modelo y se evaluó con múltiples métricas (MAE, MSE, RMSE, R², MAPE)

En la parte de regresión logística:
- Se analizó el balance de clases (212 malignos vs 357 benignos)
- Se entrenó el modelo con regularización y máximo de iteraciones
- Se evaluó con métricas de clasificación (accuracy, precision, recall, F1-score)
- Se generó la matriz de confusión para análisis detallado

## Evidencias

### Regresión Lineal ¿Qué significan estas métricas?
<img width="440" height="426" alt="image" src="https://github.com/user-attachments/assets/8e4f4bdb-9bb2-4726-8a35-52decf417ec7" />

1. MAE (Mean Absolute Error): Promedio de los errores absolutos sin importar si son positivos o negativos.
2. MSE (Mean Squared Error): Promedio de los errores al cuadrado, penaliza más los errores grandes.
3. RMSE: Raíz cuadrada del MSE, vuelve a las unidades originales del problema.
4. R²: Indica qué porcentaje de la variabilidad es explicada por el modelo (0-1, donde 1 es perfecto).
5. MAPE: Error porcentual promedio, útil para comparar modelos con diferentes escalas.

### Regresión Logística ¿Qué significan las métricas de clasificación?
<img width="652" height="670" alt="image" src="https://github.com/user-attachments/assets/43cbde52-9765-4ee8-85e0-0e374984d507" />

1. Accuracy: Porcentaje de predicciones correctas sobre el total.
2. Precision: De todas las predicciones positivas, ¿cuántas fueron realmente correctas?
3. Recall (Sensibilidad): De todos los casos positivos reales, ¿cuántos detectamos?
4. F1-Score: Promedio armónico entre precision y recall.
5. Matriz de Confusión: Tabla que muestra predicciones vs realidad.

## Dejo aquí el enlace al Google Colab donde está el análisis completo: [PRÁCTICA 4](https://colab.research.google.com/drive/1AUPagcGfYV__SJybcazNQvZVUzQkQ51B?usp=sharing)

## Reflexión
Lo más desafiante: Interpretar correctamente las diferentes métricas para cada tipo de problema y entender cuándo aplicar cada una. Las métricas de regresión (MAE, MSE, R²) son muy diferentes a las de clasificación (precision, recall, F1).

Lo más valioso: Comprender el trade-off entre precision y recall en contextos médicos, donde un falso negativo (decir que no hay cáncer cuando sí lo hay) es mucho más peligroso que un falso positivo.

Próximos pasos: Profundizar en técnicas de regularización para mejorar los modelos y experimentar con optimización de hiperparámetros para obtener mejores resultados.
