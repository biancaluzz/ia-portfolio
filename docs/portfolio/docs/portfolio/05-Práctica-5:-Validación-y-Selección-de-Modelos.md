---
title: "Entrada 05 — Práctica 5: Validación y Selección de Modelos"
date: 2025-08-26
---

# Entrada 05 — Práctica 5: Validación y Selección de Modelos

## Contexto
Implementación de técnicas de validación cruzada comparando algoritmos de clasificación para predecir el éxito académico estudiantil.

## Objetivos
- Implementar diferentes estrategias de validación cruzada (KFold vs StratifiedKFold)
- Comparar el rendimiento de múltiples algoritmos de clasificación
- Optimizar hiperparámetros usando GridSearchCV y RandomizedSearchCV
- Analizar la importancia de características para la explicabilidad del modelo

## Actividades (con tiempos estimados)
1. Configuración del entorno y carga de librerías — 10 min
2. Exploración del dataset de éxito académico estudiantil — 15 min
3. Implementación de validación cruzada KFold vs StratifiedKFold — 25 min
4. Comparación de modelos (Regresión Logística, Ridge, Random Forest) — 30 min
5. Optimización de hiperparámetros — 20 min
6. Análisis de explicabilidad e importancia de características — 20 min

## Desarrollo
La práctica se centró en predecir el éxito académico de estudiantes utilizando diferentes algoritmos de machine learning. Se trabajó con datos de 4424 estudiantes que incluían información académica, demográfica y socioeconómica.

El principal desafío fue el desbalance en los datos: solo el 56% de estudiantes se graduaba, mientras que el 29% abandonaba y el 15% seguía matriculado. Para manejar este problema, se compararon dos técnicas de validación cruzada. La técnica StratifiedKFold, que mantiene la proporción de clases en cada división de datos, demostró ser más estable y confiable que el método tradicional.

El Random Forest arrojó el mejor rendimiento con 76.6% de precisión, superando a la Regresión Logística y al Ridge Classifier. Al optimizar sus parámetros, se logró mejorar su precisión a 77.8%.

El análisis reveló que las notas del segundo semestre son el factor más importante para predecir el éxito académico, seguido de las notas de admisión y el rendimiento del primer semestre.

Este enfoque permitió no solo identificar el mejor modelo predictivo, sino también entender qué variables influyen más en el éxito académico de los estudiantes.

## Evidencias
<img width="863" height="528" alt="image" src="https://github.com/user-attachments/assets/526a3966-d134-4458-a6ce-411df8acaf5b" />

COMPARACIÓN DE ESTABILIDAD:
     StratifiedKFold es MÁS ESTABLE (menor variabilidad)
     Recomendación: Usar StratifiedKFold para este dataset

<img width="1189" height="589" alt="image" src="https://github.com/user-attachments/assets/eec59bcb-8434-4dcf-9743-4c6748c8a9cd" />

ANÁLISIS DE ESTABILIDAD:
     Logistic Regression: MUY ESTABLE (std: 0.0061)
     Ridge Classifier: MUY ESTABLE (std: 0.0032)
     Random Forest: MUY ESTABLE (std: 0.0064)

<img width="999" height="299" alt="image" src="https://github.com/user-attachments/assets/5ab2cd89-6a0f-43a8-8043-50740057d988" />

¿Cuándo usar cada método?
    GridSearchCV cuando tienes pocos hiperparámetros y mucho tiempo de cómputo.
    RandomizedSearchCV cuando tienes muchos hiperparámetros o poco tiempo limitado.
    Pipeline + SearchCV siempre previene data leaking automáticamente.
    cross_val_score en el resultado final valida que la optimización no causó overfitting.

<img width="2472" height="1190" alt="image" src="https://github.com/user-attachments/assets/f45d2a52-761c-4f04-8b79-45e59b6f876b" />

ESTADÍSTICAS DE LOS ÁRBOLES:
Profundidad promedio (primeros 5 árboles): 21.2
Número promedio de nodos (primeros 5): 1139.0

DIVERSIDAD EN EL RANDOM FOREST:
El poder del Random Forest viene de la diversidad de sus árboles:
- Cada árbol ve una muestra diferente de datos (bootstrap)
- Cada split considera solo un subconjunto aleatorio de características
- La predicción final es el voto mayoritario de todos los árboles
Usando datos sin escalar para árboles individuales

## Dejo aquí el enlace al Google Colab donde está el análisis completo: [PRÁCTICA 5](https://colab.research.google.com/drive/1Gj7JAXMHdowOcMFGTdt4rauMzbKdlYhH?usp=sharing)

## Reflexión
Lo más desafiante: Entender las diferencias entre las estrategias de validación cruzada y cuándo aplicar cada una.

Lo más valioso: Comprender que la optimización de hiperparámetros puede mejorar significativamente el rendimiento del modelo (de 76.58% a 77.83% en accuracy).

Aprendizaje clave: La validación cruzada además de ser una técnica de evaluación, también es una herramienta para entender la estabilidad y confiabilidad de nuestros modelos.

Próximos pasos: Aplicar estas técnicas a problemas de desbalance de clases más extremos.
