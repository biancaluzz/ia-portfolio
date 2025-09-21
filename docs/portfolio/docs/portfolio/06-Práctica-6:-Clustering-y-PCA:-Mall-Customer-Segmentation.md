---
title: "Entrada 06 — Práctica 6: Clustering y PCA: Mall Customer Segmentation"
date: 2025-09-02
---

# Entrada 06 — Práctica 6: Clustering y PCA: Mall Customer Segmentation

## Contexto
Implementación de técnicas de clustering para segmentar clientes de centros comerciales basándose en información demográfica y de comportamiento de compra.

## Objetivos
- Identificar 3-5 segmentos distintos de clientes usando K-Means
- Aplicar técnicas de normalización (MinMax, Standard, Robust) y comparar resultados
- Utilizar PCA para reducción de dimensionalidad y visualización
- Comparar PCA con métodos de selección de features
- Interpretar resultados desde una perspectiva de negocio

## Actividades (con tiempos estimados)
1. Configuración del entorno y carga de librerías — 10 min
2. Exploración del Mall Customer Segmentation Dataset — 20 min
3. Preprocesamiento y normalización de datos — 20 min
4. Implementación de K-Means clustering — 25 min
5. Aplicación de PCA y reducción dimensional — 20 min
6. Análisis de segmentos e interpretación de negocio — 25 min

## Desarrollo
La práctica se centró en segmentar clientes de centros comerciales utilizando técnicas de clustering no supervisado. Se trabajó con datos de 200 clientes que incluían información demográfica (edad, género) y de comportamiento (ingresos anuales, puntuación de gastos).

El principal desafío fue determinar el número óptimo de clusters y seleccionar las técnicas de preprocesamiento más adecuadas. Se compararon tres métodos de normalización (MinMax, Standard y Robust) y se encontró que MinMaxScaler proporcionaba los mejores resultados para este dataset.

El método del codo sugirió 5 clusters como número óptimo, pero tras validación con métricas de silueta, se determinó que 4 clusters proporcionaban una segmentación más adecuada.

El análisis PCA permitió reducir la dimensionalidad de 4 a 2 componentes principales que capturaban el 82.3% de la varianza, facilitando la visualización de los segmentos.

## Evidencias



## Dejo aquí el enlace al Google Colab donde está el análisis completo: [PRÁCTICA 6]([https://colab.research.google.com/drive/1Gj7JAXMHdowOcMFGTdt4rauMzbKdlYhH?usp=sharing](https://colab.research.google.com/drive/1bFpBO1SDSvFfT15RNVKFCL6-Xx1zpwVF?usp=sharing))

## Reflexión
Lo más desafiante: Determinar el número óptimo de clusters, ya que el método del codo y el análisis de silueta sugerían diferentes números óptimos.

Lo más valioso: Comprender cómo las diferentes técnicas de normalización afectan significativamente los resultados del clustering, y cómo PCA no solo ayuda en la visualización sino también en la identificación de las características más relevantes.

Aprendizaje clave: En clustering, la validación cualitativa (interpretación de negocio) es tan importante como las métricas cuantitativas.

Próximos pasos: Aplicar técnicas de clustering más avanzadas, y explorar métodos de validación más sofisticados para problemas de segmentación de clientes.
