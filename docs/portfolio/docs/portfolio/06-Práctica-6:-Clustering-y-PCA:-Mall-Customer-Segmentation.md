---
title: "Entrada 06 — Práctica 6: Clustering y PCA: Mall Customer Segmentation"
date: 2025-09-09
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

<img width="1489" height="495" alt="image" src="https://github.com/user-attachments/assets/dd22d7aa-1d07-4bf4-9cda-e918e405c36e" />

<img width="1790" height="495" alt="image" src="https://github.com/user-attachments/assets/0e8c5f1a-e618-4cdc-961a-e5a13f292f01" />

<img width="675" height="590" alt="image" src="https://github.com/user-attachments/assets/cc76ecb0-8d7e-444d-ae52-d4037fdc6d70" />

INSIGHTS PRELIMINARES - COMPLETE:

COMPLETE BASÁNDOTE EN TUS OBSERVACIONES:
   Variable con mayor variabilidad: El annual income posee la mayor STD CON 26,26K$, es la que posee mayor variabilidad
   - ¿Existe correlación fuerte entre alguna variable? Ninguna posee una correlación fuerte, pero la que posee la mayor correlación es la edad con el spending score, a mayor edad peor spending score, con un coeficiente de 0.327
   - ¿Qué variable tiene más outliers? El annual income es el unico con outliers, un total de 2 (1%)
   - ¿Los hombres y mujeres tienen patrones diferentes? Son similares, aunque en promedio parece que las mujeres ganen menos, y tengan un mejor spending score. La desvianción estandar del spending score, es mayor en los hombres, indicando que varian mas sus valores
   - ¿Qué insight es más relevante para el análisis? El diagrama de dispersión, de la relación entre el annual income, y spending score muestra una posible segmentación al observar las agrupaciones que ocurren en los datos.
   - ¿Qué 2 variables serán más importantes para clustering? Por annual income, y spending score. Por las observaciones previamente explicadas

PREPARÁNDOSE PARA CLUSTERING:
   - ¿Qué relación entre Income y Spending Score observas? Parecen ser adecuadas para el clustering debido a las agrupaciones, observadas en el grafico de dispersión
   - ¿Puedes imaginar grupos naturales de clientes? Imaginamos 5 grupos a partir de la observación del grafico de dispersión, aquellos que ganan poco, y gastan mucho, los que ganan poco y gastan poco, los que ganan en el promedio y gastan lo promedio (donde se concentran la mayoria de los valores), los que ganan mucho y gastan mucho, y por ultimo los que ganan mucho y gastan poco.

ANÁLISIS DE LAS ESTADÍSTICAS - COMPLETA:
   - ¿Qué variable tiene el rango más amplio? Annual Income (k$)
   - ¿Cuál es la distribución de género en el dataset? 40% hombres 60% mujeres
   - ¿Qué variable muestra mayor variabilidad (std)? Annual Income (k$)
   - ¿Los clientes son jóvenes o mayores en promedio? Son mas jovenes (38.8 años promedio) en comparación con los limites del rango
   - ¿El income promedio sugiere qué clase social? Media ($60.56k promedio), ya que hay gente que gana mucho y gasta poco, y viceversa.
   - ¿Por qué la normalización será crítica aca? Por los diferentes rangos de las variables.

LISTO PARA DATA PREPARATION con 5 features

<img width="1583" height="397" alt="image" src="https://github.com/user-attachments/assets/55821591-ba1b-40c0-83a8-5b9aeba310c6" />

<img width="1589" height="396" alt="image" src="https://github.com/user-attachments/assets/1ad688c2-c8a4-4bf3-accc-4371ecb21f2f" />

QUICK TEST: Impacto en Clustering (K=4)
     - MinMax: Silhouette Score = 0.364
     - Standard: Silhouette Score = 0.332
     - Robust: Silhouette Score = 0.298

GANADOR: MinMax (Score: 0.364)

¿Cuál método necesitas para obtener las etiquetas de cluster (no las distancias)?

El metodo .labels()

¿Qué significa un silhouette score más alto vs más bajo?

Un score mas bajo es menos confiable, mayor es mas confiable, debido a que estan mas definidos los clusters (mas separados unos de otros y se ve una clara división)

DECISIÓN FINAL DEL SCALER:

COMPLETE TU ANÁLISIS:
   - Mejor scaler según silhouette: MinMax
   - ¿Por qué crees que funcionó mejor? Funciono mejor debido a que los datos no poseen un rango demasiado extenso, no hay datos atipicos que puedan romper el escalamiento, por lo cual es una buena forma de escalar los valores para la segmentación.
   - ¿Algún scaler tuvo problemas obvios? Ninguno mostro problemas obvios, ya que todos poseen valores entre 0 y 1.

SCALER SELECCIONADO: MinMax
Datos preparados: (200, 5)
Listo para PCA y Feature Selection

<img width="1490" height="590" alt="image" src="https://github.com/user-attachments/assets/a93aaa37-c425-4f62-a931-8d4215c41a78" />

<img width="1190" height="790" alt="image" src="https://github.com/user-attachments/assets/f2135f4d-38e1-4867-ab3e-2811b8ef6711" />

💡 INTERPRETACIÓN DE NEGOCIO:
   - 🎯 PC1 parece representar: Diferencia por genero, basandonos en el loading, se puede ver que son los valores que mas impactan
   - 🎯 PC2 parece representar: Contraste entre edad y nivel de gasto, por las mismas razones.
   - 📊 Los clusters visibles sugieren: Existen grupos de clientes separados principalmente por género, y dentro de cada género se diferencian por edad y comportamiento de gasto

📊 COMPARACIÓN DE MÉTODOS:
   - 🏁 Baseline (todas): 0.364
   - 🔄 Forward Selection: 0.573
   - 🔙 Backward Elimination: 0.573
   - 📐 PCA (2D): 0.686

🏆 GANADOR: PCA (2D) con score = 0.686

🔍 ANÁLISIS:
   - PCA (2D): 0.686 (+88.3% vs baseline)
   - Forward Selection: 0.573 (+57.5% vs baseline)
   - Backward Elimination: 0.573 (+57.5% vs baseline)
   - Baseline (todas): 0.364 (+0.0% vs baseline)

<img width="1189" height="589" alt="image" src="https://github.com/user-attachments/assets/d6e821dc-1f8d-45ca-a4a4-0706b720047a" />

🎯 ANÁLISIS DE RESULTADOS:

🔍 FEATURES SELECCIONADAS POR CADA MÉTODO:
   - 🔄 Forward Selection: [np.str_('Spending Score (1-100)'), np.str_('Genre_Female'), np.str_('Genre_Male')]
   - 🔙 Backward Elimination: [np.str_('Spending Score (1-100)'), np.str_('Genre_Female'), np.str_('Genre_Male')]

🤝 COINCIDENCIAS:
   - Forward ∩ Backward: [np.str_('Spending Score (1-100)'), np.str_('Genre_Female'), np.str_('Genre_Male')]
   - ¿Seleccionaron las mismas features? Sí

❓ PREGUNTAS DE ANÁLISIS (completa):
   - 💡 Método con mejor score: PCA (2D) con score = 0.686
   - 📊 ¿Forward y Backward seleccionaron exactamente las mismas features? Si, Spending Score, Genre_Female y Genre_Male
   - 🤔 ¿PCA con 2 componentes es competitivo? Si, es el mejor y supera a Backward y Forward
   - 🎯 ¿Algún método superó el threshold de 0.5? Si PCA 2D, Backward y Forward lo superaron.
   - 📈 ¿La reducción de dimensionalidad mejoró el clustering? Reducir de 5 a 2 si mejoro el clustering, porque hace mas visible la división de grupos, con las 5 dimensiones el PC4 Y PC5 eran solo ruido que mas que aportar molestaba.

<img width="1489" height="590" alt="image" src="https://github.com/user-attachments/assets/dcdd894d-b434-4885-a7f6-439103781a36" />

<img width="1490" height="990" alt="image" src="https://github.com/user-attachments/assets/71a806d2-6e0a-431e-9efa-4dcb158c5b6c" />

----------------------------------------------------------------------------
### Metodología CRISP-DM:

#### ¿Qué fase fue más desafiante y por qué?
La fase más complicada fue Data Preparation, ya que se tuvo que aplicar múltiples técnicas de escalado y reducción de dimensionalidad. A partir de ello, decidir cuál era mejor para el conjunto de datos para garantizar que los reusltados fuerna óptimos para el clustering.

#### ¿Cómo el entendimiento del negocio influyó en tus decisiones técnicas?
Sabiendo que se trata de un centro comercial que busca segmentar clientes para mejorar las estrategias de marketing, se sabía que Annual Income y Spending Score iban a ser críticas.


----------------------------------------------------------------------------
### Data Preparation:

#### ¿Qué scaler funcionó mejor y por qué?
El MinMax Scaler funcionó mejor en este caso específico, obteniendo un Silhouette Score de 0.364 (vs. 0.332 de Standard y 0.298 de Robust) para K=4. Esto se debe a la naturaleza de los datos:
1. Los datos de Annual Income y Spending Score están acotados en rangos similares
2. No presentan outliers extremos.
3. MinMax asegura que todas las variables tengan el mismo peso (misma escala), evitando que una variable domine por su magnitud (ej: ingreso vs. score).

#### ¿PCA o Feature Selection fue más efectivo para tu caso?
PCA fue más efectivo porque permitió reducir la dimensionalidad manteniendo la mayor varianza posible, lo que mejoró la visualización y el rendimiento del clustering.

#### ¿Cómo balanceaste interpretabilidad vs performance?
Se utilizó PCA para mejorar la performance del modelo, pero se complementó con análisis de las componentes principales para entender qué variables originales contribuían más a cada cluster.


----------------------------------------------------------------------------
### Clustering:

#### ¿El Elbow Method y Silhouette coincidieron en el K óptimo?
Sí, ambos métodos sugirieron que el número óptimo de clusters era 5.

#### ¿Los clusters encontrados coinciden con la intuición de negocio?
Sí, los clusters representaron segmentos claros como clientes de alto ingreso y gasto, clientes de bajo ingreso y gasto, y clientes de comportamiento medio.

#### ¿Qué harías diferente si fueras a repetir el análisis?
Tal vez probar con otros algoritmos de clustering para poder comparar resultados.


----------------------------------------------------------------------------
### Aplicación Práctica:

#### ¿Cómo presentarías estos resultados en un contexto empresarial?
Para presentar resultados siempre conviene tener visualizaciones claras con gráficos, acompañado con un informe que resuma los segmentos encontrados, descripción y recomendaciones.

#### ¿Qué valor aportan estas segmentaciones?
- Optimizar campañas de marketing dirigidas a grupos específicos.
- Asignar recursos de manera más eficiente.
- Mejorar la experiencia del cliente con ofertas personalizadas.
- Incrementar la retención y el gasto promedio por cliente.

#### ¿Qué limitaciones tiene este análisis?
La data utilizada contiene 200 registros y podría no ser representativa de todos. Las variables utilizadas son básicas, estaría bueno incluir atributos de comportamiento.

----------------------------------------------------------------------------

## Dejo aquí el enlace al Google Colab donde está el análisis completo: [PRÁCTICA 6](https://colab.research.google.com/drive/1bFpBO1SDSvFfT15RNVKFCL6-Xx1zpwVF?usp=sharing)

## Reflexión
Lo más desafiante: Determinar el número óptimo de clusters, ya que el método del codo y el análisis de silueta sugerían diferentes números óptimos.

Lo más valioso: Comprender cómo las diferentes técnicas de normalización afectan significativamente los resultados del clustering, y cómo PCA no solo ayuda en la visualización sino también en la identificación de las características más relevantes.

Aprendizaje clave: En clustering, la validación cualitativa (interpretación de negocio) es tan importante como las métricas cuantitativas.

Próximos pasos: Aplicar técnicas de clustering más avanzadas, y explorar métodos de validación más sofisticados para problemas de segmentación de clientes.
