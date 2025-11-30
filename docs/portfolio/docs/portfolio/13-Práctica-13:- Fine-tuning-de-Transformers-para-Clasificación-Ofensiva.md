---
title: "Entrada 13 — Práctica 13: Fine-tuning de Transformers para Clasificación Ofensiva"
date: 2025-11-04
---

# 😀 Análisis de Sentimiento en Noticias Financieras usando Transformers

## Contexto
Implementación de un modelo de clasificación de sentimiento para noticias financieras utilizando el dataset zeroshot/twitter-financial-news-sentiment y el modelo BERT. El objetivo fue clasificar tweets financieros en tres categorías: Bearish (0), Bullish (1) y Neutral (2).

## Objetivos
- Cargar y explorar un dataset de sentimiento financiero en inglés.
- Preprocesar los datos y adaptarlos a un modelo Transformer (BERT).
- Entrenar y evaluar un clasificador de sentimiento utilizando la biblioteca transformers de Hugging Face.
- Analizar el rendimiento del modelo y reflexionar sobre su aplicabilidad en contextos financieros.

## Actividades (con tiempos estimados)
1. Configuración del entorno e instalación de bibliotecas (10 min).
2. Carga y exploración del dataset (15 min).
3. Preprocesamiento y tokenización de los textos (20 min).
4. Entrenamiento y evaluación del modelo BERT (45 min).
5. Análisis de resultados y reflexión (20 min).

## Desarrollo
Se utilizó el dataset zeroshot/twitter-financial-news-sentiment, que contiene tweets financieros etiquetados en tres categorías de sentimiento. El dataset se dividió en entrenamiento (9,543 ejemplos) y validación (2,388 ejemplos).

## Evidencias

0.  $BYND - JPMorgan reels in expectations on Beyo...      0

1.  $CCL $RCL - Nomura points to bookings weakness...      0
2.  $CX - Cemex cut at Credit Suisse, J.P. Morgan ...      0
3.  $ESS: BTIG Research cuts to Neutral https://t....      0
4.  $FNKO - Funko slides after Piper Jaffray PT cu...      0
label
2.    6178
1.    1923
0.    1442

<img width="540" height="394" alt="image" src="https://github.com/user-attachments/assets/cfc47022-592f-4e62-a2ba-7afb893355c8" />

- ¿Cómo es la distribución de longitudes? ¿Qué implica para el truncation del tokenizer? La distribución muestra que la mayoría de textos tienen entre 5-20 tokens, con muy pocos superando 25 tokens. Esto confirma que un max_length de 128 es más que suficiente y que incluso podría disminuirse y funcionar.
- ¿Las clases están balanceadas? ¿Cómo afectará esto a las métricas y al entrenamiento? Las clases están desbalanceadas: Clase 2 (Neutral) = 6,178 (65%), Clase 1 (Bullish) = 1,923 (20%), Clase 0 (Bearish) = 1,442 (15%). Por este desbalance, el modelo tiende a favorecer a la clase mayoritaria.

<img width="471" height="311" alt="image" src="https://github.com/user-attachments/assets/27b5604b-c48f-49ec-85f4-2f2b980bf19e" />

Top n-grams para clase 0:
co: 737
https co: 735
https: 735
to: 383
the: 321
in: 267
of: 233
on: 224
as: 175
after: 171

Top n-grams para clase 1:
co: 852
https: 842
https co: 842
to: 492
on: 387
the: 349
in: 324
up: 269
stock: 258
at: 215

Top n-grams para clase 2:
co: 3559
https: 3518
https co: 3518
the: 1892
to: 1787
of: 1255
in: 1058
for: 882
on: 762
and: 760

<img width="636" height="350" alt="image" src="https://github.com/user-attachments/assets/45fcf054-4af7-433b-ad8a-6ca0f8673517" />

- ¿Qué n-grams son más frecuentes por clase? ¿Te sorprenden?
  - Clase 0 (Bearish): "after", "cut", "down" - términos negativos esperados
  - Clase 1 (Bullish): "up", "stock", "gain" - términos positivos claros
  - Clase 2 (Neutral): vocabulario general como "the", "to", "of"
- ¿Qué sesgos/ruido ves en las nubes de palabras? "https" y "co" dominan todas las clases, sugiriendo que URLs/tickers son ruido que debería limpiarse.

<img width="617" height="451" alt="image" src="https://github.com/user-attachments/assets/4523ca96-1bd8-4e2d-b298-40cfa323a361" />

<img width="617" height="451" alt="image" src="https://github.com/user-attachments/assets/b5ae4832-8bd3-4260-94af-15b4e4cf3280" />

- ¿Hay separabilidad en PCA/UMAP? Si no, ¿por qué? ¿Datos solapados, ruido, features?
  - PCA revela cierta estructura pero con áreas de mezcla
  - UMAP muestra un solapamiento significativo
  - El solapamiento sugiere que el contexto y relaciones semánticas complejas son importantes.
- ¿Los vecinos de Word2Vec reflejan semántica financiera? No reflejan semántica financiera.

              precision    recall  f1-score   support

           0       0.59      0.64      0.61       288
           1       0.72      0.73      0.72       385
           2       0.88      0.86      0.87      1236

    accuracy                           0.80      1909
   macro avg       0.73      0.74      0.74      1909
weighted avg       0.81      0.80      0.80      1909

<img width="392" height="316" alt="image" src="https://github.com/user-attachments/assets/78cb888b-5bd7-4353-9db8-14727add7346" />

- ¿En qué clases falla más el baseline? ¿Por qué?
  - Clase 0 (Bearish): F1 más bajo (0.61) - clase minoritaria más difícil
  - Clase 1 (Bullish): Performance media (0.72)
  - Clase 2 (Neutral): Mejor performance (0.87) - beneficio del desbalance
- ¿Qué hiperparámetros probaste y cómo cambiaron los resultados?
  - class_weight='balanced' fue acertado dado el desbalance
  - ngram_range=(1,2) capturó bigramas importantes como "price target", "stock up"
  - max_features=10000 no sobrecarga el modelo

Epoch	Training Loss	Validation Loss	Accuracy	F1

1	0.476500	0.403554	0.862232	0.809617

2	0.262600	0.388149	0.871661	0.826117

3	0.149000	0.469289	0.870613	0.827613

- ¿Cuánto mejora el Transformer al baseline? ¿Dónde empeora?
  - Accuracy: 87.1% (+7 puntos vs baseline)
  - Macro F1: 82.8% (+9.3 puntos vs baseline)
  - Mejora consistente en todas las métricas
- ¿Qué costo de entrenamiento observaste (tiempo/VRAM)? Tiempo de ~12 minutos

<img width="576" height="455" alt="image" src="https://github.com/user-attachments/assets/6017dd0f-2d57-4679-af6c-216f72b4b2c5" />

- ¿Cuál método elegirías para producción y por qué? FinBERT.
  - FinBERT entiende contexto financiero específico
  - Mejor manejo de lenguaje financiero técnico
  - Superior discriminación entre Bullish/Bearish
- ¿Qué siguientes pasos intentarías (data cleaning, RAG, ajuste de clases)? El primer paso urgente sería una limpieza de datos, eliminando URLs, menciones, símbolos de trading.

## Dejo aquí el enlace al Google Colab donde está el análisis completo: [PRÁCTICA 13](https://colab.research.google.com/drive/1Ff3za3Mgi-Oz7XhtuTgldWH0KRjDFjrg?usp=sharing)

## Reflexión
Lo más desafiante: Ajustar el modelo BERT para un dominio específico como las noticias financieras, ya que uso términos técnicos.

Lo más valioso: Poder aplicar un modelo complejo como BERT a un problema real de clasificación de sentimiento con la ayuda de la biblioteca transformers.

Aprendizaje clave: Los modelos preentrenados como BERT son extremadamente versátiles y pueden adaptarse a dominios específicos con relativamente pocos datos.

Próximos pasos: Experimentar con fine-tuning en datasets más grandes o en otros idiomas.
