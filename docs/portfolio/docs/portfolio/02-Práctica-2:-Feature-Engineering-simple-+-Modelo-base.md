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
<img width="443" height="299" alt="image" src="https://github.com/user-attachments/assets/0b856a44-8e0f-44c0-a860-ec701a30e714" />

**Matriz de confusión: ¿En qué casos se equivoca más el modelo: cuando predice que una persona sobrevivió y no lo hizo, o al revés?**
Observando los resultados arrojados, se equivoca más en falsos negativos, personas que el modelo predijo que no sobrevivieron, pero en realidad sí, siendo 21 casos. Frente a 12 casos de falsos positivos, personas que el modelo predijo que sobrevivieron pero en realidad murieron.

**Clases atendidas: ¿El modelo acierta más con los que sobrevivieron o con los que no sobrevivieron?**
- Clase 0 (no sobrevivió) tiene un recall de 89%, acierta bien en identificar no supervivientes.
- Clase 1 (sobrevivió) tiene un recall de 70%, tiene mayores dificultades para identificar todos los supervivientes reales.

El modelo es mejor prediciendo no supervivencia (89% vs. 70%).

**Comparación con baseline: ¿La Regresión Logística obtiene más aciertos que el modelo que siempre predice la clase más común?**
Sí, tiene más aciertos. La Baseline tiene una accuracy de 61.45%, mientras que la LogReg tiene una accuracy de 81.56%.

**Errores más importantes: ¿Cuál de los dos tipos de error creés que es más grave para este problema?**
En este caso, por la cantidad de falsos negativos, y siendo que es crucial idenitficar a todos los posibles supervivientes en caso de necesitar un rescate, es mas grave la cantidad de personas que el modelo predijo que no sobrevivieron, pero en realidad sí.

**Observaciones generales: Mirando las gráficas y números, ¿qué patrones interesantes encontraste sobre la supervivencia?**
- Hay un desbalance en los datos, clase 0 (no sobrevivió) tiene 110 casos, mientras clase 1 (sobrevivió) solamente 69 casos, por lo que puede llevar a predecir mejor a la clase 0.
- El equilibrio entre precision y recall (f1-score) es alto en ambas clases, siendo un poco mejor en clase 0 de 86%, ante 74% de clase 1. Por lo que para la clase 1, pierde aproximadamente un 30% de los supervivientes reales.

**Mejoras simples: ¿Qué nueva columna (feature) se te ocurre que podría ayudar a que el modelo acierte más?**
Estaría bueno categorizar las edades entre niños, adultos, adultos mayores para visualizar con mayor claridad la supervivencia. También, podría ser analizar teniendo en cuenta los datos de familiares, ya que puede arrojar algunos patrones grupales.


## Dejo aquí el enlace al Google Colab donde está el análisis completo: [PRÁCTICA 2](https://colab.research.google.com/drive/1mN_pvPaqD5K8tMUzzK7OV6Xvknqat-mH?usp=sharing)

## Reflexión
Lo más desafiante: interpretar la matriz de confusión para entender los tipos de errores del modelo.

Lo más valioso: poder establecer una línea base para validar el modelo a partir de patrones reales.

Próximos pasos: probar modelos más complejos.
