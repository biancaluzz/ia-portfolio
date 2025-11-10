---
title: "Entrada 11 — Práctica 11: YOLOv8 Fine-tuning & Tracking"
date: 2025-09-07
---

# 🔍 Detección de Objetos con YOLO: Del Modelo Base al Fine-Tuning

## Contexto
Implementación y evaluación del modelo YOLOv8 para detección de objetos en imágenes de supermercado, explorando las limitaciones de modelos pre-entrenados y el proceso de adaptación mediante fine-tuning para dominios específicos.

## Objetivos
- Configurar el entorno para trabajar con YOLOv8 y realizar inferencias básicas
- Evaluar el desempeño del modelo base (COCO) en imágenes de productos de supermercado
- Entender las limitaciones de conjuntos de datos genéricos para casos de uso específicos
- Preparar el pipeline para fine-tuning en datasets especializados

## Actividades (con tiempos estimados)
1. Setup del entorno e instalación de dependencias (15 min)
2. Carga y evaluación del modelo YOLOv8 base (20 min)
3. Análisis de inferencias en imágenes de grocery (40 min)
4. Preparación para fine-tuning y reflexión sobre limitaciones (50 min)

## Desarrollo
Se implementó YOLOv8 nano como modelo base pre-entrenado en el dataset COCO, que contiene 80 clases genéricas de objetos. Se realizaron inferencias en imágenes de pasillos de supermercado para evaluar su desempeño en detección de productos específicos.

El modelo base demostró capacidades limitadas para identificar productos específicos de supermercado, detectando principalmente categorías genéricas como "naranjas" y "brócoli" pero sin capacidad para distinguir entre variedades específicas o productos empaquetados.

## Evidencias
=== MODELO BASE (COCO) ===
Clases en COCO: 80
Ejemplos de clases: ['person', 'bicycle', 'car', 'motorcycle', 'airplane', 'bus', 'train', 'truck', 'boat', 'traffic light', 'fire hydrant', 'stop sign', 'parking meter', 'bench', 'bird', 'cat', 'dog', 'horse', 'sheep', 'cow']

Clases 'grocery' en COCO: ['apple', 'orange', 'banana', 'carrot', 'bottle', 'cup', 'bowl']
⚠️ Nota: COCO tiene clases genéricas, no productos específicos

1. ¿Por qué elegimos YOLOv8n (nano) en lugar de modelos más grandes?

velocidad, es más rápido para pruebas iniciales y consume menos recursos

2. ¿Cuántas clases tiene COCO? ¿Son suficientes para nuestro caso de uso?

80 clases de objetos comunes (personas, autos, animales, frutas, utensilios, etc.).

3. ¿Qué significa que COCO tenga "clases genéricas"?

Significa que las categorías son muy amplias y no distinguen entre variantes o marcas.

4. Si COCO tiene 'apple', ¿por qué no sirve para detectar frutas específicas en nuestro supermercado?

Porque aprendió una sola categoría “apple”, no las distintas variedades o presentaciones de manzanas No generaliza a productos reales de góndola, donde la iluminación, empaques y etiquetas son diferentes.

=== INFERENCIA CON MODELO BASE ===

image 1/1 /content/grocery_aisle.jpg: 480x640 3 oranges, 2 broccolis, 238.8ms
Speed: 25.6ms preprocess, 238.8ms inference, 12.6ms postprocess per image at shape (1, 3, 480, 640)

<img width="841" height="658" alt="image" src="https://github.com/user-attachments/assets/84ef236f-77fa-43ef-b4a6-d91c6205ee2c" />

📊 Objetos detectados: 5
  1. orange: 0.367
  2. orange: 0.297
  3. orange: 0.289
  4. broccoli: 0.235
  5. broccoli: 0.216

¿Cuántos productos detectó el modelo base?
Detectó 4 productos.

¿Las detecciones son correctas? ¿Son específicas?
Ninguna detección es correcta. Si, son especificas.

¿Por qué crees que el modelo base no funciona bien para productos específicos de grocery?
Porque usa COCO, y esta no tiene clases genéricas.

¿Qué clases detecta que NO son útiles para nuestro caso de uso?
Detecta frutas, y en este caso de uso debería detectar verduras.

=== CONFIGURACIÓN DEL DATASET ===
Número de clases: 6
Clases: ['Apple', 'Banana', 'Grape', 'Orange', 'Pineapple', 'Watermelon']
Train path: E:\DL\attempt1\attempt3\datasets\Fruits-detection-1\train\images
Val path: E:\DL\attempt1\attempt3\datasets\Fruits-detection-1\valid\images

📊 ESTADÍSTICAS FINALES:
  Train images: 0
  Val images: 0
  Total: 0
  Clases: 6

=== EXPLORANDO DATASET ===
Train labels: fruit_detection/Fruits-detection/train/labels
Val labels: fruit_detection/Fruits-detection/valid/labels

=== DISTRIBUCIÓN DE CLASES (TRAIN) ===
Total de clases: 6
Clases del dataset: ['Apple', 'Banana', 'Grape', 'Orange', 'Pineapple', 'Watermelon']

Apple               : 6070 instancias
Banana              : 2971 instancias
Grape               : 6027 instancias
Orange              : 13938 instancias
Pineapple           : 1372 instancias
Watermelon          : 1683 instancias

<img width="1189" height="590" alt="image" src="https://github.com/user-attachments/assets/b44a257c-a03f-4244-8395-788bcfa7fd74" />

📊 ESTADÍSTICAS ADICIONALES:
  Instancias totales: 32061
  Promedio por clase: 5343.5
  Clase más frecuente: Orange (13938 instancias)
  Clase menos frecuente: Pineapple (1372 instancias)

¿Las clases están balanceadas? ¿Qué problemas podría causar un desbalance?
Sí, están desbalanceadas. Por lo que tiende a detectar mejor los datos de las clases de las que tiene más datos.

¿Qué clase tiene más instancias? ¿Crees que el modelo será mejor detectando esa clase?
Orange tiene más instancias. Sí, es más probable que sea mejor.

¿La clase con menos instancias podría tener más errores? ¿Por qué?
Sí, podría tener más errores. Porque al tener más información de las otras clases, va a ser mejor detectando patrones para las demás.

Si tuvieras que agregar más datos, ¿qué clase priorizarías y por qué?
Sería ideal priorizar a las clases con menos instancias: Watermelon, Pineapple y Bananana. De esta manera será mejor detectandolas. Aunque depende del caso de uso, si tu propósito es detectar solo naranjas, es mejor agregar instancias acá.

=== VISUALIZANDO EJEMPLOS ===
Encontradas 7108 imágenes de training
<img width="1545" height="1590" alt="image" src="https://github.com/user-attachments/assets/ae3643ac-41a0-443f-a792-51a7f916755a" />

¿Las bounding boxes se ven bien ajustadas a las frutas?
Son bastante precisas, aunque en el caso de la manzana, al estar recortada la imagen, también aparece recortada la detección de la bounding box. Además, como se tratan de rectangulos, se adapta a la forma de todos los alimentos.

¿Hay frutas que se solapan? ¿Cómo podría afectar esto al modelo?
Sí, por ejemplo las uvas. Al solaparse podría no interpretar correctamente la forma de la fruta, o al estar recortada no reconocer de qué se trata.

¿Las imágenes tienen buena variedad (tamaños, ángulos, iluminación)?
Sí, pareciera que eligieron imágenes con diferentes ángulos y calidad, también aparecen las frutas cortadas e igual las reconoce

¿Notaste alguna anotación incorrecta o faltante?
El bounding box de la manzana no muestra el nombre de la fruta, ya que se ajustó lo máximo posible para tomar toda la unidad de la manzana. También en el caso de las uvas, las que se encuentran más alejadas, no son reconocidas por el modelo.

=== RESULTADOS DEL TRAINING ===

<img width="2400" height="1200" alt="image" src="https://github.com/user-attachments/assets/632fe3a8-5adc-45c4-8178-76079f13ef84" />
box_loss (Loss de Localización):
1. ¿Qué mide esta métrica? Mide el error en la predicción de las coordenadas y dimensiones de los bounding boxes (cajas delimitadoras).
2. ¿Cómo evolucionó durante el training (aumentó o disminuyó)? Disminuyó consistentemente de 1.159 (epoch 1) a 0.7921 (epoch 20)
3. ¿Por qué queremos que esta métrica sea baja? Una box_loss baja significa que el modelo está prediciendo bounding boxes más precisos y mejor alineados con los objetos reales.

cls_loss (Loss de Clasificación):
1. ¿Qué aspecto de la detección mide? Mide el error en la clasificación de los objetos (identificar correctamente si es Apple, Banana, etc.).
2. Si cls_loss es alto, ¿qué problema tiene el modelo? El modelo tendría dificultad para distinguir entre las diferentes clases de frutas.
3. ¿Observaste mejoras epoch tras epoch? Disminuyó drásticamente de 3.082 a 0.8556.

dfl_loss (Distribution Focal Loss):
1. ¿Esta métrica refina la predicción de bounding boxes? Si
2. ¿Qué relación tiene con la precisión de las coordenadas? Refina la localización de bounding boxes mediante distribución de probabilidades. Ayuda a predecir coordenadas más precisas.
3. ¿Debería ser alta o baja al final del training? Definitivamente baja, como se observa al final del training.

Instances:
1. ¿Qué representa este número en cada batch? El número de objetos (instancias) detectados en cada batch de entrenamiento.
2. ¿Por qué varía entre batches? Diferentes batches tienen diferentes cantidades de objetos. El dataset no está balanceado en términos de objetos por imagen.

GPU_mem:
1. ¿Cuánta memoria GPU usó tu training? Estabilizado en ~4.62GB (desde epoch 10 en adelante)
2. ¿Qué pasaría si te quedas sin memoria GPU? Training se detendría con error.

Convergencia:
1. ¿El modelo convergió (las losses dejaron de bajar)? Sí, pero podría mejorar más. Las losses todavía mostraban tendencia decreciente al final.
2. ¿Cuántos epochs necesitó para estabilizarse? Aproximadamente 15 epochs para mostrar mejoras consistentes.
3. Si tuvieras más tiempo, ¿entrenarías más epochs? Sí.


=== CARGANDO MODELO FINE-TUNED ===
Path: /content/runs/detect/fruit_finetuned/weights/last.pt

✅ Modelo fine-tuned cargado
   Clases: ['Apple', 'Banana', 'Grape', 'Orange', 'Pineapple', 'Watermelon']
   Total de clases: 6

📊 Comparación:
   Modelo base (COCO): 80 clases (genéricas)
   Modelo fine-tuned: 6 clases (frutas específicas)
   Mejora: Especializado en detección de frutas

=== EVALUACIÓN EN VALIDATION SET ===
Ultralytics 8.3.227 🚀 Python-3.12.12 torch-2.8.0+cu126 CUDA:0 (Tesla T4, 15095MiB)
Model summary (fused): 72 layers, 3,006,818 parameters, 0 gradients, 8.1 GFLOPs
val: Fast image access ✅ (ping: 0.0±0.0 ms, read: 1610.3±437.6 MB/s, size: 63.0 KB)
val: Scanning /content/fruit_detection/Fruits-detection/valid/labels.cache... 914 images, 0 backgrounds, 0 corrupt: 100% ━━━━━━━━━━━━ 914/914 1.4Mit/s 0.0s
val: /content/fruit_detection/Fruits-detection/valid/images/3d3ddc3054b32eb7_jpg.rf.03e7789aaf5212e2634b84ef502e0832.jpg: 1 duplicate labels removed
                 Class     Images  Instances      Box(P          R      mAP50  mAP50-95): 100% ━━━━━━━━━━━━ 58/58 4.0it/s 14.3s
                   all        914       3227      0.534      0.365       0.38      0.241
                 Apple        188        557      0.541      0.352      0.384      0.268
                Banana        167        390      0.533       0.39       0.41      0.229
                 Grape        199        809        0.5       0.32      0.325      0.196
                Orange        197       1100      0.555      0.349       0.37      0.233
             Pineapple         77        154      0.535      0.367      0.342      0.208
            Watermelon        107        217      0.541      0.415      0.447       0.31
Speed: 2.5ms preprocess, 4.4ms inference, 0.0ms loss, 1.9ms postprocess per image
Results saved to /content/runs/detect/val

📊 MÉTRICAS DEL MODELO FINE-TUNED:
  mAP@0.5:     0.380
  mAP@0.5:0.95: 0.241
  Precision:   0.534
  Recall:      0.365

=== MÉTRICAS POR CLASE ===
Apple               : mAP@0.5 = 0.268
Banana              : mAP@0.5 = 0.229
Grape               : mAP@0.5 = 0.196
Orange              : mAP@0.5 = 0.233
Pineapple           : mAP@0.5 = 0.208
Watermelon          : mAP@0.5 = 0.310

¿Qué significa mAP@0.5? ¿Por qué es importante?
mAP (Precisión Media Promedio) de Detección de Objetos. Porque indica la precisión a la hora de identificar la clase y refleja la mejora que ha tenido nuestro modelo en su aprendizaje.

¿Cuál es la diferencia entre mAP@0.5 y mAP@0.5:0.95? ¿Cuál es más estricto?
Que mAP@0.5:0.95 es más exigente en la variación. Por lo que es más estricto, ya que requiere una mayor superposición para las posibles coincidencias

Si Precision es alta pero Recall es bajo, ¿qué problema tiene el modelo?
Muchos falsos negativos.

Si Recall es alto pero Precision es baja, ¿qué significa?
Muchos falsos positivos.

La precisión es cuántos de los casos positivos son verdaderamente positivos (tiene en cuenta TP/(TP+FP)).

El recall es cuántos de los casos negativos son verdadermanete negativos, por lo que la precisión se ve penalizada por los falsos positivos (tiene en cuenta TN/(TN+FN))

¿Qué clase tiene el mejor mAP? ¿Coincide con la clase más frecuente del dataset?
No, es watermelon la que tiene mejor mAP, pero es la segunda con menos datos. Parece ser que es más sencillo de detectar el patrón de watermelon que de otras frutas, por lo que con menos datos es más fácil de identificar.

=== COMPARACIÓN: BASE vs FINE-TUNED ===
Comparando en 3 imágenes del validation set


============================================================
Imagen 1/3: 064c52456bdf03af_jpg.rf.f584a76d2d0613f16dc9bbe7477bec5b.jpg
  Modelo Base (COCO):  13 detecciones
  Modelo Fine-tuned:    3 detecciones
  Diferencia:          -10
  Clases (Base):       banana, person, truck
  Clases (Fine-tuned): Banana

<img width="1525" height="788" alt="image" src="https://github.com/user-attachments/assets/08565fc8-a111-4ddc-8094-83420619733d" />

============================================================
Imagen 2/3: aa4b88b1f645dfc1_jpg.rf.8ae7c2c9a7f15ee97dd85b66f026e919.jpg
  Modelo Base (COCO):   1 detecciones
  Modelo Fine-tuned:    2 detecciones
  Diferencia:          +1
  Clases (Base):       banana
  Clases (Fine-tuned): Banana

<img width="1525" height="788" alt="image" src="https://github.com/user-attachments/assets/b4b08045-0c3e-49d3-8dcd-e6d907a323a0" />

============================================================
Imagen 3/3: 0e427c3df6d2dec1_jpg.rf.d78fbe8a085150f7aeb0779d3809f999.jpg
  Modelo Base (COCO):   2 detecciones
  Modelo Fine-tuned:    1 detecciones
  Diferencia:          -1
  Clases (Base):       vase, apple
  Clases (Fine-tuned): Apple

<img width="1525" height="788" alt="image" src="https://github.com/user-attachments/assets/5da6090c-4929-4ed3-a2a5-0c6b442258b7" />

============================================================

¿El modelo fine-tuned detectó más frutas que el base? ¿Por qué? Sí, pero no consistentemente. En la imagen 1, el fine-tuned detectó 2 frutas mientras el base detectó 0. Sin embargo, en las otras imágenes el base detectó más objetos. Esto porque el modelo fine-tuned está especializado en frutas específicas.

¿Hubo frutas que el modelo base detectó pero el fine-tuned no? ¿Cómo lo explicas? Sí, debido a falsos positivos del modelo base o sobre especialización del fine-tuned.

¿Las bounding boxes del modelo fine-tuned se ven más ajustadas? Sí.

¿Notaste diferencias en las confidence scores entre ambos modelos? El fine-tuned tiene confidence scores más altos para frutas específicas.

¿Qué tipo de errores sigue cometiendo el modelo fine-tuned? Falsos negativos, sensibilidad a variaciones, problemas con frutas superpuestas.

=== ANÁLISIS DE ERRORES ===

=== RESULTADOS COMPARATIVOS ===

Modelo Base (COCO):
  TP: 0, FP: 16, FN: 23
  Precision: 0.000
  Recall:    0.000
  F1-Score:  0.000

Modelo Fine-tuned:
  TP: 4, FP: 2, FN: 19
  Precision: 0.667
  Recall:    0.174
  F1-Score:  0.276

=== MEJORA ===
  Δ Precision: +0.667
  Δ Recall:    +0.174
  Δ F1-Score:  +0.276

<img width="989" height="590" alt="image" src="https://github.com/user-attachments/assets/12e87391-94f1-4b53-89b3-b20b3503cb11" />

¿Cuánto mejoró el mAP después del fine-tuning?
Precisión: de 0.000 → 0.667 (+0.667)
Recall: de 0.000 → 0.174 (+0.174)
F1-Score: de 0.000 → 0.276 (+0.276)
¿Qué clases de productos tienen mejor detección? ¿Cuáles peor?
MEJOR: Clases con más True Positives (4 detecciones correctas)
PEOR: Clases con muchos False Negatives (19 no detectados)
¿Los False Positives disminuyeron? ¿Y los False Negatives?
False Positives: 16 → 2 (Reducción del 87.5%)
False Negatives: 23 → 19 (Mejora del 17%)
¿El fine-tuning justificó el tiempo y esfuerzo? Sí, pasó de ser un modelo inútil a un modelo funcional.

¿Qué ajustes harías para mejorar aún más el modelo? Data augmentation, reducir umbral de confianza, balancear el dataset.


¿Por qué distance_threshold=100 píxeles? ¿Cómo se relaciona con el tamaño del frame? En frames de 640x480, 100px representa ~15% del ancho. Permite movimiento normal entre frames sin perder tracking.

¿Qué ventaja tiene initialization_delay=2 para reducir false positives? Reduce falsos positivos, requiere 2 detecciones consecutivas.

Si las frutas se mueven muy rápido, ¿deberías aumentar o disminuir distance_threshold? Aumentar distance_threshold (150-200px) porque los objetos rápidos se mueven más entre frames.

¿Qué significa que un track "sobreviva" 30 frames sin detección? El track sigue vivo aunque el objeto desaparezde temporalmente. 30 frames = 1 segundo.

¿Cuándo activarías filtros de Kalman? ¿Qué beneficio dan para predicción de movimiento? Activar cuando los objetos se mueven con patrones predecibles. Predice la posición futura.


Visualizar Video con Tracking

¿Los IDs se mantienen consistentes para cada fruta? No, hay diferentes IDs para mismas frutas

¿Hay "ID switches" (una fruta cambia de ID)? Sí.

¿Qué frutas se detectan mejor? La banana y la naranja

¿Hay falsos positivos o negativos? Hay falsos negativos, ya que no detecta todo el tiempo las manzanas o bananas.

📊 Estadísticas generales:
  Total productos trackeados: 13
  Duración promedio: 55.8 frames (1.9s)
  Duración máxima: 297 frames (9.9s)
  Duración mínima: 4 frames (0.1s)

📋 Detalle por producto trackeado:
Track ID     Clase                Duración        Rango Frames        
----------------------------------------------------------------------
Track 1      Orange                217 frames ( 7.2s)    2 → 218 
Track 2      Apple                  14 frames ( 0.5s)    4 → 17  
Track 3      Apple                   4 frames ( 0.1s)    9 → 12  
Track 4      Banana                297 frames ( 9.9s)   46 → 342 
Track 5      Apple                   4 frames ( 0.1s)   80 → 83  
Track 6      Orange                 18 frames ( 0.6s)   82 → 99  
Track 7      Apple                   8 frames ( 0.3s)   87 → 94  
Track 8      Apple                  12 frames ( 0.4s)  173 → 184 
Track 9      Apple                  44 frames ( 1.5s)  188 → 231 
Track 10     Banana                 16 frames ( 0.5s)  257 → 272 
Track 11     Orange                 10 frames ( 0.3s)  262 → 271 
Track 12     Orange                 30 frames ( 1.0s)  286 → 315 
Track 13     Orange                 51 frames ( 1.7s)  292 → 342 

📦 Productos por clase:
  Apple               :   6 tracks
  Orange              :   5 tracks
  Banana              :   2 tracks

<img width="1590" height="1190" alt="image" src="https://github.com/user-attachments/assets/00f4afb9-84d4-4eea-bc48-7d6b198c7291" />

⚡ Métricas de calidad del tracking:
  Tracks cortos (<1s):  8 (61.5%)
  Tracks largos (>3s):  2 (15.4%)
  Tracks totales:       13

¿Cuántos productos diferentes se trackearon en el video? 13 IDs
Apple: 6
Orange: 5
Banana: 2
¿Los IDs se mantuvieron consistentes o hubo switches? Mismo producto cambia de ID múltiples veces.

¿Qué productos tienen tracking más estable? ¿Cuáles menos?

MÁS ESTABLE: Banana (Track 4 - 9.9s) y Orange (Track 1 - 7.2s)
MENOS ESTABLE: Apple (múltiples tracks cortos <0.5s)
¿Cómo podrías mejorar la estabilidad del tracking?
Reducir distance_treshold para mas precisión.
Aumentar hit_counter_max para mayor tolerancia a oclusiones.
¿Este sistema sería útil para tu aplicación de retail? ¿Qué ajustes harías? Es útil para conteo de productos, para ello es necesarios reducir los ID switches, y mejorar la detección de clases problemáticas (Apple).

## 🎯 Reflexión Final: Integrando Todo el Assignment

Sobre el Modelo:

1. ¿Cuál fue la mejora más significativa del fine-tuning? (mAP, FPs, FNs): Precisión de 0% → 67% (el modelo pasó de inútil a funcional)

2. ¿El modelo base (COCO) era completamente inútil o tenía algo de valor? COCO proporcionó features generales que aceleraron el fine-tuning, demostrando que el transfer learning es eficiente.

3. Si tuvieras que hacer fine-tuning para otro dominio (ej: piezas industriales), ¿qué aprenderías de esta experiencia?  La estrategia de fine-tuning progresivo funciona.


Sobre los Datos:

1. ¿8,479 imágenes es mucho o poco para fine-tuning? ¿Por qué funcionó usar solo 25%? Suficiente para fine-tuning gracias al transfer learning. El 25% funcionó porque el modelo ya tenía features básicas de COCO.

2. ¿La calidad de las anotaciones afectó los resultados? ¿Cómo lo sabes? Afectó directamente el recall bajo - algunas frutas no se detectaban por anotaciones incompletas o difíciles.

3. Si pudieras agregar 1,000 imágenes más, ¿de qué tipo serían? Priorizaría casos difíciles: oclusiones, iluminación variable, ángulos atípicos y la clase con peor performance.


Sobre el Tracking:

1. ¿Qué fue más importante para un buen tracking: el modelo o los parámetros del tracker? Primero el modelo (sin buenas detecciones no hay tracking), luego los parámetros del tracker.

2. ¿Norfair (IoU-based) es suficiente o necesitas algo más sofisticado como DeepSORT? Norfair es suficiente para casos simples, pero DeepSORT sería mejor para objetos similares usando apariencia visual.

3. ¿Los filtros de Kalman mejoraron la estabilidad del tracking? ¿En qué situaciones? Mejoraron con movimiento predecible (cinta transportadora), menos con objetos estáticos o movimiento errático.

4. ¿En qué escenarios fallaría este sistema de tracking? Oclusiones prolongadas, cambios bruscos de movimiento, objetos muy similares visualmente.


Sobre el Deployment:

1. ¿Este sistema podría correr en tiempo real? ¿Qué FPS necesitarías?
¿Qué optimizaciones harías para producción? (modelo, código, hardware) Sí, con optimizaciones (YOLOv8s, TensorRT).

2. ¿Cómo manejarías casos extremos? (oclusiones, iluminación, ángulos raros) Data augmentation específica, múltiples cámaras, reglas de negocio para casos ambiguos.


Trade-offs y Decisiones:

1. Identifica 3 trade-offs clave que encontraste (ej: speed vs accuracy, epochs vs tiempo)
- Accuracy vs Speed: Modelo más preciso = más lento
- Recall vs Precision: Más detecciones = más falsos positivos
- Training time vs Performance: Más epochs = mejor modelo pero más costo

2. ¿Cuál fue la decisión más importante que tomaste en los hyperparámetros? Learning rate 1e-5 para fine-tuning

3. Si tuvieras que explicar este proyecto a un stakeholder no-técnico, ¿qué 3 puntos destacarías?
- Automatiza conteo y tracking de productos
- Reduce errores humanos en inventario
- Escalable para múltiples tiendas con bajo costo marginal


## Dejo aquí el enlace al Google Colab donde está el análisis completo: [PRÁCTICA 11](https://colab.research.google.com/drive/1tdq81F_iBwAnhh5AKkgkjX96GEBgCeeu?usp=sharing)

## Reflexión
Lo más desafiante: Entender las limitaciones prácticas de modelos pre-entrenados en dominios específicos y la necesidad de adaptación mediante fine-tuning.

Lo más valioso: La experiencia práctica de evaluar un modelo en escenarios reales y visualizar directamente sus fortalezas y debilidades.

Aprendizaje clave: Los modelos genéricos requieren especialización para aplicaciones específicas mediante transfer learning y datasets domain-specific.

Próximos pasos: Implementar fine-tuning con dataset especializado de productos de supermercado y evaluar mejora en precisión para el dominio específico.
