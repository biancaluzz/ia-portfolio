---
title: "Entrada 08 — Práctica 8: Experimentación"
date: 2025-09-23
---

# 🧪 Experimentación Sistemática con Redes Neuronales

## Contexto
Experimentación exhaustiva con diferentes arquitecturas de redes neuronales, optimizadores y técnicas de regularización para maximizar el accuracy en el dataset CIFAR-10.

## Objetivos
- Realizar experimentación sistemática variando arquitecturas de redes neuronales
- Probar diferentes técnicas de regularización (Dropout, BatchNorm, L2)
- Evaluar múltiples optimizadores y sus hiperparámetros
- Lograr el mejor accuracy posible en CIFAR-10 usando MLP

## Actividades (con tiempos estimados)
1. Preparación del entorno y dataset CIFAR-10 (10 min)
2. Experimentación con arquitecturas (80 min)

## Desarrollo
Se implementó una metodología de experimentación sistemática basada en la guía proporcionada, probando combinaciones de:

🧪 Arquitecturas Probadas
- Capas densas: Desde 2 hasta 5 capas
- Funciones de activación: ReLU, GELU, Tanh
- Normalización: BatchNormalization entre capas
- Regularización: Dropout (0.0-0.5) y L2 (1e-5 a 1e-4)
- Inicializadores: HeNormal, GlorotUniform

⚙️ Optimizadores Evaluados
- Adam: Learning rates 1e-2 a 5e-4
- SGD con momentum: Momentum 0.0-0.95, Nesterov
- RMSprop: Variación de learning_rate y rho
- AdamW: Weight decay 1e-5 a 1e-4

⏱️ Callbacks Implementados
- EarlyStopping: Paciencia 15 épocas, restore_best_weights
- ReduceLROnPlateau: Factor 0.5, paciencia 8 épocas
- TensorBoard: Monitoreo en tiempo real

## Evidencias
🎯 Resultados TensorFlow:
  - Training Accuracy: 52.3%
  - Test Accuracy: 49.3%
  - Parámetros totales: 1,742,474

## Dejo aquí el enlace al Google Colab donde está el análisis completo: [PRÁCTICA 8](https://colab.research.google.com/drive/1oCZ_Pl2YhQtMZLrKQeOJMgJXAg-AHo1q?usp=sharing)

## Reflexión
Lo más desafiante: Ver cómo después de estar rato exprimentando, no poder superar cierto umbral.

Lo más valioso: La experiencia práctica de probar sistemáticamente diferentes configuraciones y ver su impacto real en el rendimiento. 

Aprendizaje clave: La elección de arquitectura debe alinearse con la naturaleza de los datos. A veces, mejor tuning no puede superar las limitaciones de la arquitectura.

Próximos pasos: Explorar arquitecturas convolucionales (CNN) que están específicamente diseñadas para imágenes y deberían superar significativamente estos resultados.
