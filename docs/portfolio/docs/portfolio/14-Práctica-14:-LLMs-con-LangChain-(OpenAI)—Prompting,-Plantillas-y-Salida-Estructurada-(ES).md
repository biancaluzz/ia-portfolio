---
title: "Entrada 14 — Práctica 14: LLMs con LangChain (OpenAI) — Prompting, Plantillas y Salida Estructurada (ES)"
date: 2025-11-11
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
