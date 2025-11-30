---
title: "Entrada 17 — Vertex"
date: 2025-11-25
---

# 📐 Vertex AI Pipelines

## Contexto
Esta práctica me introdujo al mundo de MLOps con Vertex AI Pipelines, explorando cómo automatizar y reproducir flujos completos de machine learning en Google Cloud. A diferencia de enfoques tradicionales donde cada paso del proceso de ML se maneja manualmente, Vertex AI Pipelines permite orquestar todo el ciclo de vida del modelo mediante componentes containerizados que garantizan reproducibilidad y escalabilidad.

## Objetivos
El objetivo principal fue comprender y construir pipelines de ML escalables usando Kubeflow Pipelines SDK. 

## Actividades (con tiempos estimados)
1. Configuración inicial (5 min)
2. Pipeline introductorio (5 min)
3. Pipeline completo AutoML (10 min)
4. Ejecución y monitoreo (20 min)
5. Análisis de métricas (10 min):

## Desarrollo
La experiencia comenzó con la configuración del entorno en Vertex AI Workbench, instalando las bibliotecas esenciales como Kubeflow Pipelines SDK y Google Cloud Pipeline Components.

En la primera fase, se construyó un pipeline introductorio compuesto por tres componentes.

Posteriormente, se implementó un pipeline completo de machine learning para clasificación tabular utilizando el dataset Dry Beans de UCI Machine Learning.

La ejecución del pipeline permitió observar la integración con los servicios de Vertex AI.

La práctica culminó con el análisis comparativo de múltiples ejecuciones de pipelines utilizando DataFrames de Pandas.

## Evidencias
![Imagen de WhatsApp 2025-11-25 a las 20 24 49_b2ee8af8](https://github.com/user-attachments/assets/2e2b7ef5-0669-421f-b911-83f679953673)
![Imagen de WhatsApp 2025-11-25 a las 20 46 32_55213f48](https://github.com/user-attachments/assets/dd0bcd0a-d3d7-4912-8c50-e7bf0ea596ac)
<img width="818" height="206" alt="image" src="https://github.com/user-attachments/assets/7da36eed-aca7-49b7-8afa-9cf586ee40bc" />

## Reflexión
Lo más desafiante: comprender la arquitectura de componentes y cómo estos se comunican mediante inputs y outputs en el grafo de ejecución.

Lo más valioso: capacidad de crear pipelines completamente automatizados que toman decisiones inteligentes sobre el despliegue de modelos basándose en métricas.

Aprendizaje clave:  los pipelines de ML no son solo secuencias de pasos, sino sistemas de toma de decisiones automatizadas.

Próximos pasos: explorar pipelines más complejos con múltiples modelos y experimentar con diferentes estrategias de deployment.
