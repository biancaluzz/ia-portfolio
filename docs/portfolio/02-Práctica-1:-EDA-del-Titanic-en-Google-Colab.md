---
title: "Entrada 02 — Práctica 1: EDA del Titanic en Google Colab"
date: 2025-08-12
---

# Entrada 02 — Práctica 1: EDA del Titanic en Google Colab

## Contexto
Actividad introductoria a los datasets.

## Objetivos
- Entender cómo se compone el dataset
- Crear gráficos a partir de los datos
- Llegar a conclusiones a partir de la información procesada

## Actividades (con tiempos estimados)
- 0. Investigación del Dataset del Titanic (10 min)
- 1. Setup en Colab (5 min)
- 2. Cargar el dataset de Kaggle (2 opciones) (5-10 min)
- 3. Conocer el dataset (10 min)
- 4. EDA visual con seaborn/matplotlib (15 min)

## Desarrollo
La práctica 1 se basó en comprender profundamente los datos, limpiarlos y descubrir patrones visuales iniciales.

Se comenzó analizando y entendiendo que el dataset contiene información de los pasajeros del Titanic. Se indetificaron los datos disponibles y definió Survived como variable objetivo.

Luego de configurar el entorno de Google Colab, se accedió a los archivos y librerías necesarias.

Algunas funciones utilizadas:
- shape -> dimensiones
- head() -> visualizar primeras filas
- info() -> tipos de datos de cada columna
- describe() -> estadísticas descriptivas
- isna().sum() -> cuantificación de valores faltantes

Se crearon múltiples gráficos para identificar relaciones:
- Countplot
- Barplot
- Histograma
- Mapa de calor

## Evidencias
- Dejo aquí el enlace al Google Colab PRÁCTICA 1: https://colab.research.google.com/drive/1mN_pvPaqD5K8tMUzzK7OV6Xvknqat-mH?usp=sharing

## Reflexión
Lo más desafiante: entender los datos que tengo enfrente, y saber lidiar con los datos faltantes.

Lo más valioso: interpretar la información a través de la visualización en gráficos.

Próximos pasos: hacer un análisis más profundo cruzando diferentes variables.
