---
title: "Entrada 10 — Práctica 10: Data Augmentation Avanzado & Explicabilidad"
date: 2025-10-14
---

# 🌸 Data Augmentation Avanzado & Explicabilidad: Clasificación de Flores

## Contexto
Implementación de pipelines de data augmentation avanzado y técnicas de explicabilidad para mejorar la clasificación de flores del dataset Oxford Flowers102 usando transfer learning con EfficientNet.

## Objetivos
- Implementar pipelines de data augmentation con Keras layers
- Aplicar transfer learning con EfficientNetB0 para clasificación de 102 especies de flores
- Utilizar técnicas de explicabilidad (Grad-CAM) para entender las decisiones del modelo
- Comparar el rendimiento con y sin data augmentation avanzado

## Actividades (con tiempos estimados)
1. Setup y carga del dataset Oxford Flowers102 (30 min)
2. Implementación de pipelines de data augmentation (45 min)
3. Entrenamiento con transfer learning y fine-tuning (60 min)
4. Análisis de explicabilidad con Grad-CAM (45 min)

## Desarrollo
Se implementaron dos pipelines principales para el dataset Oxford Flowers102:
- Pipeline Baseline: Preprocesamiento básico con normalización EfficientNet
- Pipeline Avanzado: Data augmentation con transformaciones geométricas (flip, rotation, zoom, translation) y fotométricas (brightness, contrast)

Se utilizó EfficientNetB0 con fine-tuning en las capas finales, logrando clasificación multiclase para las 102 especies de flores. Las técnicas de Grad-CAM permitieron visualizar qué regiones de las imágenes eran más relevantes para las predicciones del modelo.

## Evidencias

Dataset oxford_flowers102 downloaded and prepared to /root/tensorflow_datasets/oxford_flowers102/2.1.1. Subsequent calls will reuse this data.
✅ Dataset descargado:
   Train: 1020 imágenes
   Test: 6149 imágenes
   Clases: 102

✅ Datasets preparados:
   Train subset: 5000
   Test subset: 1000
   Rango de píxeles: [0, 255] (antes de normalización)

🎨 VISUALIZACIÓN: Data Augmentation
   Nota: Visualización usa imágenes [0, 255] ANTES de normalización
<img width="1456" height="1475" alt="image" src="https://github.com/user-attachments/assets/7c81e44a-33ff-4294-a08c-17886e9bcbc3" />

## 🎯 Reflexión Final:

- Data Augmentation: El aumento de datos ayuda a prevenir overfitting y mejora la generalización, especialmente importante en datasets pequeños como el de flores.

- GradCAM: Permite verificar si el modelo está aprendiendo características relevantes de las flores (pétalos, centro) en lugar de patrones irrelevantes.

- Errores del Modelo: Al analizar errores con GradCAM, podemos identificar si el modelo se confunde por fondos similares o características compartidas entre especies.

- Aplicación Práctica: En una app de identificación de flores, la explicabilidad es crucial para generar confianza en los usuarios y validar que el modelo funciona correctamente.

- Mejoras: Fine-tuning del modelo base, más datos de entrenamiento, y experimentar con diferentes técnicas de aumento de datos podrían mejorar aún más el rendimiento.

## Dejo aquí el enlace al Google Colab donde está el análisis completo y la implementación del modelo propio: [PRÁCTICA 10](https://colab.research.google.com/drive/1eAiS-PlZpinHKu7_l5rb-JBoa9zBULPS?usp=sharing)

##Reflexión
Lo más desafiante: Crear el modelo propio desde 0.

Lo más valioso: Ver cómo Grad-CAM revela que el modelo realmente aprende características específicas en lugar de patrones superficiales.

Aprendizaje clave: El data augmentation bien diseñado puede ser más efectivo que arquitecturas complejas para mejorar generalización en dominios específicos.

Próximos pasos: Experimentar con técnicas de auto-augmentation y aplicar estas metodologías a otros datasets de imágenes especializadas.
