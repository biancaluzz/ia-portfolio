---
title: "Entrada 12 — Práctica 12: Segmentación Semántica con Segment Anything Model (SAM)"
date: 2025-10-28
---

# 📌 Segmentación Semántica con SAM: Explorando Modelos de Segmentación Zero-Shot

## Contexto
Implementación del modelo Segment Anything (SAM) de Meta para realizar segmentación semántica en imágenes de áreas inundadas. El objetivo fue explorar las capacidades de un modelo de segmentación zero-shot en un dataset real de detección de agua.

## Objetivos
- Configurar el entorno y descargar el dataset de segmentación de áreas inundadas
- Explorar y visualizar el dataset con imágenes y máscaras binarias
- Implementar SAM para generar segmentaciones automáticas
- Evaluar el rendimiento del modelo en tareas de segmentación semántica
- Comparar diferentes estrategias de segmentación (automática vs. con prompts)

## Actividades (con tiempos estimados)
1. Configuración del entorno e instalación de dependencias (15 min)
2. Descarga y preparación del dataset Kaggle (20 min)
3. Exploración y análisis del dataset de inundaciones (50 min)
4. Implementación de SAM para segmentación (30 min)
5. Evaluación y visualización de resultados (20 min)

## Desarrollo
Se descargó el dataset "Flood Area Segmentation" de Kaggle, que contiene 290 imágenes y sus respectivas máscaras binarias. El dataset mostró una gran variabilidad en tamaños de imagen (81 tamaños únicos) con un ratio promedio de píxeles de agua del 42.8%.

Se implementó SAM utilizando tanto el modo automático (SamAutomaticMaskGenerator) como el modo con prompts (SamPredictor). El modelo demostró capacidad para segmentar áreas de agua sin entrenamiento previo específico, aprovechando su entrenamiento zero-shot en 11 millones de imágenes.

## Evidencias
=== DATASET CARGADO ===
Total images: 100
Image shape (primera imagen): (551, 893, 3)
Mask shape (primera máscara): (551, 893)

📊 Estadísticas del dataset:
Tamaños únicos de imágenes: 81

Water pixel ratio (promedio): 42.80%
Background ratio: 57.20%

<img width="1589" height="1058" alt="image" src="https://github.com/user-attachments/assets/495422e4-2a8f-4c8d-8d5b-12a407228b09" />

=== POINT PROMPT PREDICTION ===
Point: (1, 369)
Confidence score: 0.965

<img width="1589" height="256" alt="image" src="https://github.com/user-attachments/assets/0e23a3a8-282c-4201-82a8-3a6e20f2ccbd" />

=== BOX PROMPT PREDICTION ===
Box: [np.int64(0), np.int64(129), np.int64(928), np.int64(522)]
Confidence score: 0.989

<img width="1589" height="256" alt="image" src="https://github.com/user-attachments/assets/c379a2cf-b437-420e-9067-c3f09ee1d5e6" />

=== MÉTRICAS - POINT PROMPT ===
IoU: 0.8070
Dice: 0.8932
Precision: 0.9681
Recall: 0.8290

=== MÉTRICAS - BOX PROMPT ===
IoU: 0.8016
Dice: 0.8899
Precision: 0.9756
Recall: 0.8180

=== COMPARACIÓN ===
Box prompt better: False

=== EVALUATING PRETRAINED SAM (Point Prompts) ===
  Processed 20/100 images...
  Processed 40/100 images...
  Processed 60/100 images...
  Processed 80/100 images...
  Processed 100/100 images...

=== PRETRAINED SAM - POINT PROMPTS ===
Mean IoU: 0.5291 ± 0.3214
Mean Dice: 0.6220 ± 0.3377
Mean Precision: 0.8193
Mean Recall: 0.5885

=== EVALUATING PRETRAINED SAM (Box Prompts) ===
  Processed 20/100 images...
  Processed 40/100 images...
  Processed 60/100 images...
  Processed 80/100 images...
  Processed 100/100 images...

=== PRETRAINED SAM - BOX PROMPTS ===
Mean IoU: 0.7230 ± 0.2088
Mean Dice: 0.8156 ± 0.1985
Mean Precision: 0.8476
Mean Recall: 0.8106

<img width="1389" height="990" alt="image" src="https://github.com/user-attachments/assets/5b149115-fc59-4e55-99e8-252493fe2ad7" />

=== DATALOADERS CREADOS ===
Train batches: 40
Val batches: 10

Sample batch:
  Images shape: torch.Size([2, 3, 1024, 1024])
  Masks shape: torch.Size([2, 1, 1024, 1024])
  Prompts: 2 items

✅ Loss functions definidas
Test loss: 0.6532

=== FINE-TUNING SETUP ===
Total parameters: 93,735,472
Trainable parameters: 4,058,340
Trainable %: 4.33%

Optimizer: Adam
Learning rate: 0.0001
Scheduler: StepLR (decay every 5 epochs by 0.5)

=== TRAINING COMPLETED ===
Best Val IoU: 0.7495

<img width="1389" height="490" alt="image" src="https://github.com/user-attachments/assets/ef91750c-fa75-4598-bacc-8dd573101eef" />

=== EVALUATING FINE-TUNED SAM ===
  Processed 20/20 images...

=== FINE-TUNED SAM ===
Mean IoU: 0.7335 ± 0.1895
Mean Dice: 0.8291 ± 0.1585
Mean Precision: 0.9024
Mean Recall: 0.7810

=== COMPARISON ===
Metric          Pretrained      Fine-tuned      Improvement    
------------------------------------------------------------
IOU             0.5291          0.7335          38.63          %
DICE            0.6220          0.8291          33.30          %
PRECISION       0.8193          0.9024          10.15          %
RECALL          0.5885          0.7810          32.70          %

<img width="1389" height="990" alt="image" src="https://github.com/user-attachments/assets/01794615-49c0-4616-9350-76a1fa3e3ecf" />


<img width="1489" height="861" alt="image" src="https://github.com/user-attachments/assets/e7041196-111c-46c8-b900-f6e5c44b60ec" />
=== IMAGE 0 ===
Pretrained: IoU=0.0018, Dice=0.0036
Fine-tuned: IoU=0.7105, Dice=0.8308
Improvement: IoU +0.7087, Dice +0.8271

<img width="1489" height="894" alt="image" src="https://github.com/user-attachments/assets/bfa7e2f0-029b-490f-ac7a-85f5c4535f1b" />
=== IMAGE 5 ===
Pretrained: IoU=0.5862, Dice=0.7391
Fine-tuned: IoU=0.8472, Dice=0.9173
Improvement: IoU +0.2610, Dice +0.1782

<img width="1489" height="848" alt="image" src="https://github.com/user-attachments/assets/01d4811c-a7ec-484e-99f0-fb7d7d28a058" />
=== IMAGE 10 ===
Pretrained: IoU=0.9338, Dice=0.9658
Fine-tuned: IoU=0.9292, Dice=0.9633
Improvement: IoU +-0.0046, Dice +-0.0025

<img width="1489" height="930" alt="image" src="https://github.com/user-attachments/assets/7c761335-8879-45c3-ae14-bc0d3cad2b53" />
=== IMAGE 15 ===
Pretrained: IoU=0.2934, Dice=0.4537
Fine-tuned: IoU=0.3025, Dice=0.4645
Improvement: IoU +0.0091, Dice +0.0108

=== ANALYZING PRETRAINED FAILURES ===
Failure cases: 7

Failure statistics:
  Mean IoU: 0.092
  Mean water region width: 1.00 pixels

<img width="1489" height="436" alt="image" src="https://github.com/user-attachments/assets/5c658d11-ba85-4a2e-9034-80c821d4f321" />

=== ANALYZING FINE-TUNED FAILURES ===
Failure cases: 2

=== FAILURE REDUCTION ===
Pretrained failures: 7
Fine-tuned failures: 2
Reduction: 5 (71.4%)

## Preguntas de Reflexión

1. ¿Por qué el pretrained SAM puede fallar en detectar agua en imágenes de inundaciones efectivamente? El pretrained SAM fue entrenado principalmente en objetos con boundaries bien definidos, mientras que el agua de inundaciones tiene características diferentes: boundaries difusos, texturas homogéneas, reflejos que confunden, y variabilidad en apariencia (agua clara vs. turbia).

2. ¿Qué componentes de SAM decidiste fine-tunear y por qué? ¿Por qué congelamos el image encoder? Solo el mask decoder porque es suficiente para adaptar el modelo a la tarea específica manteniendo la eficiencia. Congelamos el image encoder porque: (1) ya captura features visuales genéricas útiles, (2) es computacionalmente costoso reentrenarlo, y (3) el prompt encoder + mask decoder son suficientes para aprender las características específicas del agua.

3. ¿Cómo se comparan point prompts vs box prompts en este caso de uso de flood segmentation? Point prompts son más eficientes para este caso porque el agua suele formar regiones conectadas donde un punto es suficiente. Box prompts pueden capturar mejor áreas dispersas pero requieren más precisión del usuario. En implementación automática, points son más fáciles de generar programáticamente.

4. ¿Qué mejoras específicas observaste después del fine-tuning? (boundaries del agua, false positives, reflections, etc.) Mejora en boundaries difusos del agua, reducción de falsos positivos en áreas reflectantes, mejor detección de agua turbia o con sedimentos, y mayor robustez frente a variaciones de iluminación y sombras.

5. ¿Este sistema está listo para deployment en un sistema de respuesta a desastres? ¿Qué falta? No completamente. Faltaría validación en datos de diferentes regiones geográficas, integración con fuentes de datos en tiempo real, entre otros.

6. ¿Cómo cambiaría tu approach si tuvieras 10x más datos? ¿Y si tuvieras 10x menos? Entrenaría más componentes (incluyendo parcialmente el image encoder). Con 10x menos usaría transfer learning más agresivo.

7. ¿Qué desafíos específicos presenta la segmentación de agua en inundaciones? Reflejos que parecen agua, sombras que oscurecen el agua real, objetos flotantes que interrumpen la superficie, agua turbia que se confunde con terreno.

## Dejo aquí el enlace al Google Colab donde está el análisis completo: [PRÁCTICA 12](https://colab.research.google.com/drive/158e0cgHRZ5u8DKDac9JdWL71Ly5askjU?usp=sharing)

## Reflexión
Lo más desafiante: Manejar la gran variabilidad de tamaños en el dataset, requiriendo preprocesamiento adaptativo.

Lo más valioso: Experimentar con un modelo de segmentación como SAM y ver su capacidad para generalizar a dominios no vistos durante su entrenamiento.

Aprendizaje clave: Los modelos zero-shot como SAM representan un avance significativo en visión por computadora, permitiendo aplicaciones específicas sin necesidad de fine-tuning excesivo.

Próximos pasos: Experimentar con fine-tuning de SAM en el dataset específico y comparar el rendimiento con arquitecturas tradicionales de segmentación semántica como U-Net.
