---
title: "Entrada 09 — Práctica 9: Redes Convolucionales y Transfer Learning"
date: 2025-09-30
---

# 🎯 Redes Convolucionales y Transfer Learning: Del Cero a la Reutilización Inteligente

## Contexto
Implementación y comparación de dos enfoques fundamentales en visión por computadora: una CNN construida desde cero y un modelo de Transfer Learning utilizando MobileNetV2, aplicados ambos al dataset CIFAR-10 para clasificación de imágenes.

## Objetivos
- Implementar una CNN simple desde cero para clasificar imágenes CIFAR-10
- Aplicar Transfer Learning con MobileNetV2 pre-entrenado en ImageNet
- Comparar el rendimiento, complejidad y eficiencia de ambos enfoques
- Analizar overfitting y capacidad de generalización de cada modelo

## Actividades (con tiempos estimados)
1. Setup y configuración del entorno - Importar librerías y verificar GPU (10 min)
2. Preparación del dataset CIFAR-10 - Carga y preprocesamiento (25 min)
3. Implementación de CNN simple - Arquitectura y compilación (40 min)
4. Transfer Learning con MobileNetV2 - Configuración y fine-tuning (35 min)
5. Entrenamiento comparativo - Ambos modelos con callbacks (50 min)
6. Evaluación y análisis - Métricas, visualización y conclusiones (30 min)

Desarrollo
Se configuró el entorno TensorFlow/Keras con semillas para reproducibilidad. El sistema utilizó CPU para el procesamiento, asegurando accesibilidad independiente del hardware disponible.

📊 Dataset CIFAR-10
- 50,000 imágenes de entrenamiento y 10,000 de test
- Dimensiones: 32x32 píxeles con 3 canales de color (RGB)
- 10 clases: airplane, automobile, bird, cat, deer, dog, frog, horse, ship, truck
- Normalización: valores de 0-255 escalados a 0-1
- Codificación one-hot para las etiquetas

## Evidencias
<img width="755" height="607" alt="image" src="https://github.com/user-attachments/assets/c4522ee6-9b44-40ab-b826-cccc377ac5fb" />
<img width="826" height="446" alt="image" src="https://github.com/user-attachments/assets/76ac638f-9446-4922-9650-c096034129fd" />
📊 EVALUACIÓN FINAL
--------------------------------------------------
📊 COMPARACIÓN FINAL:
🏗️ CNN Simple: 0.7100 (71.00%)
🎯 Transfer Learning: 0.2860 (28.60%)
📈 Mejora: -42.40%
313/313 ━━━━━━━━━━━━━━━━━━━━ 4s 13ms/step
313/313 ━━━━━━━━━━━━━━━━━━━━ 9s 25ms/step
<img width="1990" height="1190" alt="image" src="https://github.com/user-attachments/assets/1319afcd-3d77-4231-a56b-9c3f5df43ead" />
🔍 ANÁLISIS DE OVERFITTING:
🏗️ CNN Simple - Gap Train-Val: 0.175
🎯 Transfer Learning - Gap Train-Val: 0.005
⚠️ CNN Simple muestra overfitting significativo

📋 REPORTE DE CLASIFICACIÓN - CNN SIMPLE:
              precision    recall  f1-score   support

    airplane       0.79      0.73      0.76      1000
  automobile       0.77      0.85      0.81      1000
        bird       0.64      0.60      0.62      1000
         cat       0.53      0.52      0.53      1000
        deer       0.68      0.66      0.67      1000
         dog       0.59      0.61      0.60      1000
        frog       0.82      0.72      0.77      1000
       horse       0.71      0.81      0.75      1000
        ship       0.87      0.78      0.82      1000
       truck       0.73      0.82      0.78      1000

    accuracy                           0.71     10000
   macro avg       0.71      0.71      0.71     10000
weighted avg       0.71      0.71      0.71     10000


📋 REPORTE DE CLASIFICACIÓN - TRANSFER LEARNING:
              precision    recall  f1-score   support

    airplane       0.26      0.31      0.29      1000
  automobile       0.31      0.22      0.26      1000
        bird       0.31      0.11      0.16      1000
         cat       0.33      0.18      0.23      1000
        deer       0.37      0.29      0.33      1000
         dog       0.20      0.18      0.19      1000
        frog       0.31      0.48      0.38      1000
       horse       0.28      0.33      0.30      1000
        ship       0.30      0.28      0.29      1000
       truck       0.26      0.49      0.34      1000

    accuracy                           0.29     10000
   macro avg       0.29      0.29      0.28     10000
weighted avg       0.29      0.29      0.28     10000

## Dejo aquí el enlace al Google Colab donde está el análisis completo: [PRÁCTICA 9](https://colab.research.google.com/drive/1TVykEP6nMtihJ3gQcZ9_zEqbi0RBL2ch?usp=sharing)

## Reflexión
Lo más desafiante: Entender por qué el Transfer Learning falló tan significativamente.

Lo más valioso: La comparación práctica entre construir desde cero versus aprovechar conocimiento pre-existente, mostrando que no hay solución universal.

Aprendizaje clave: La importancia de adaptar los modelos pre-entrenados al dominio específico y que el tamaño de entrada es crítico para el éxito del Transfer Learning.

Próximos pasos: Probar diferentes arquitecturas pre-entrenadas mejor adaptadas a imágenes.
