---
title: "Entrada 02 — Práctica 2: Feature Engineering simple + Modelo base"
date: 2025-08-12
---

# Entrada 02 — Práctica 2: Feature Engineering simple + Modelo base

## Contexto
Actividad de modelado predictivo y evaluación de algoritmos de machine learning.

## Objetivos
- Construir un modelo de clasificación.
- Establecer una línea base y evaluar el rendimiento del modelo con métricas.

## Actividades (con tiempos estimados)
0. Investigación de Scikit-learn (10 min)
1. Preprocesamiento y features (15 min)
2. Modelo base y baseline (20 min)

## Desarrollo
La práctica 2 se centró en la preparación de datos y la construcción de un modelo de machine learning para predecir la supervivencia de pasajeros.

Se aplicó un preprocesamiento:
- Se completaron los valores faltantes: Usando la mediana para 'Sex' y 'Pclass' para la edad, y la moda para 'Embarked'.
- Se crearon nuevas variables: 'FamilySize', 'IsAlone' y extracción de 'Title'.

Se utilizó train_test_split para dividir los datos (80/20). 

Se estableció un baseline con DummyClassifier para comparar con el modelo de Regresión.

El modelo fue evaluado con:
- classification_report para precisión, recall y F1-score.
- confusion_matrix para analizar falsos positivos/negativos.

## Evidencias
- Dejo aquí el enlace al Google Colab donde está el análisis completo: [PRÁCTICA 2](https://colab.research.google.com/drive/1mN_pvPaqD5K8tMUzzK7OV6Xvknqat-mH?usp=sharing)

## Reflexión
Lo más desafiante: interpretar la matriz de confusión para entender los tipos de errores del modelo.

Lo más valioso: poder establecer una línea base para validar el modelo a partir de patrones reales.

Próximos pasos: probar modelos más complejos.
