---
title: "Entrada 01 — Práctica 1: EDA del Titanic en Google Colab"
date: 2025-08-12
---

# Entrada 01 — Práctica 1: EDA del Titanic en Google Colab

## Contexto
Actividad introductoria de análisis exploratorio de datos (EDA) utilizando el dataset de Titanic de Kaggle.

## Objetivos
- Entender cómo se compone el dataset
- Crear gráficos a partir de los datos
- Llegar a conclusiones a partir de la información procesada

## Actividades (con tiempos estimados)
0. Investigación del Dataset del Titanic (10 min)
1. Setup en Colab (5 min)
2. Cargar el dataset de Kaggle (2 opciones) (5-10 min)
3. Conocer el dataset (10 min)
4. EDA visual con seaborn/matplotlib (15 min)

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
<img width="1189" height="989" alt="image" src="https://github.com/user-attachments/assets/e9e256fd-586f-4393-b3a6-32e6869858a1" />

1. ¿Qué variables parecen más relacionadas con Survived? 
Se observa una fuerte relacion entre el sexo y el grado de supervivencia, ya que la mayoria de las personas que no sobrevivieron fueron hombres. Por otro lado, la clase también tiene una tendencia, siendo que hay mayor supervivencia en 1era clase, seguido por segunda clase, y menor la supervivencia de la 3era clase.

2. ¿Dónde hay más valores faltantes? ¿Cómo los imputarías? Observando los resultados arrojados por: "print(train.isna().sum().sort_values(ascending=False))"
Hay una gran cantidad de datos faltantes en:
    - Cabin, numero de cabina: como hay tantos faltantes tal vez es un dato que se puede descartar para el análisis, ya que con tanto dato nulo es dificil llegar a conclusiones certeras.
    - Age, edad: imputar utilizando la edad promedio, para así no afectar significativamente los resultados.

4. ¿Qué hipótesis probarías a continuación? Al encontrar que las mujeres sobreviven más y las personas de la 1era clase también, comprobar si también se mantiene este grado de supervivencia más alto para las mujeres en la primera clase.

### Dejo aquí el enlace al Google Colab donde está el análisis completo: [PRÁCTICA 1](https://colab.research.google.com/drive/1mN_pvPaqD5K8tMUzzK7OV6Xvknqat-mH?usp=sharing)

## Reflexión
Lo más desafiante: entender los datos que tengo enfrente, y saber lidiar con los datos faltantes.

Lo más valioso: interpretar la información a través de la visualización en gráficos.

Próximos pasos: hacer un análisis más profundo cruzando diferentes variables.
