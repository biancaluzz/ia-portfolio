---
title: "Entrada 07 — Práctica 7: De Perceptrón a Redes Neuronales"
date: 2025-09-16
---

# 🧠 Del Perceptrón a las Redes Neuronales: Descifrando los Límites y Potencial del Aprendizaje Profundo

## Contexto
Implementación de un perceptrón (unidad básica de una red neuronal) para resolver compuertas lógicas, para lograr entender cómo funciona un clasificador lineal y visualizar cómo aprende a separar diferentes datos.

## Objetivos
- Crear un perceptrón desde cero que pueda resolver AND y OR
- Ver gráficamente cómo el perceptrón traza una línea para separar los datos
. Entender cómo los pesos y el sesgo afectan las decisiones del modelo
- Descubrir qué problemas puede y no puede resolver un perceptrón simple

## Actividades (con tiempos estimados)
1. Preparación del entorno - Definir las funciones del perceptrón (10 min)
2. Resolver AND - Encontrar pesos que funcionen y visualizar (20 min)
3. Resolver OR - Ajustar los parámetros para OR y visualizar (20 min)
4. Comparar resultados - Analizar diferencias y limitaciones (30 min)

## Desarrollo
Se implementó un perceptrón de manera manual, probando diferentes combinaciones de pesos y sesgo hasta encontrar las que resolvían perfectamente las compuertas AND y OR. Para cada compuerta:
- AND: Produce salida 1 solo cuando AMBAS entradas son 1
- OR: Produce salida 1 cuando AL MENOS UNA entrada es 1

Se encontró que con pesos de 0.5 para ambas entradas, solo era necesario ajustar el sesgo:
- AND: Sesgo = -0.7 (comportamiento más estricto)
- OR: Sesgo = -0.2 (comportamiento más permisivo)

Ambos modelos alcanzaron 100% de precisión, clasificando correctamente las cuatro combinaciones posibles de entradas (00, 01, 10, 11).

## Evidencias
1️⃣ PROBLEMA AND: Solo verdadero cuando AMBAS entradas son 1

x1 | x2 | AND esperado

 0 |  0 |      0

 0 |  1 |      0

 1 |  0 |      0

 1 |  1 |      1

Probando AND con pesos: w1=0.5, w2=0.5, bias=-0.7
  - 0,0 → 0 (esperado 0) ✅
  - 0,1 → 0 (esperado 0) ✅
  - 1,0 → 0 (esperado 0) ✅
  - 1,1 → 1 (esperado 1) ✅

  <img width="707" height="556" alt="image" src="https://github.com/user-attachments/assets/05d82b0d-d0ad-432a-b009-3084537feba5" />

🔍 Interpretación: Los puntos ROJOS (○) son clase 0, los AZULES (■) son clase 1
   La línea VERDE separa las clases.

💡 Recordá: Un perceptrón es la ecuación de una línea: y = w₁x₁ + w₂x₂ + b

2️⃣ PROBLEMA OR: Verdadero cuando AL MENOS UNA entrada es 1

x1 | x2 | OR esperado

 0 |  0 |      0

 0 |  1 |      1

 1 |  0 |      1

 1 |  1 |      1

Probando OR con pesos: w1=0.5, w2=0.5, bias=-0.2
  - 0,0 → 0 (esperado 0) ✅
  - 0,1 → 1 (esperado 1) ✅
  - 1,0 → 1 (esperado 1) ✅
  - 1,1 → 1 (esperado 1) ✅

  <img width="707" height="556" alt="image" src="https://github.com/user-attachments/assets/8b1ae4b4-12d0-4347-81b1-a9e585a7ea67" />


3️⃣ PROBLEMA NOT: Inversor simple

x | NOT esperado

0 |      1

1 |      0

Probando NOT con peso: w1=-1, bias=0.5
  - 0 → 1 (esperado 1) ✅
  - 1 → 0 (esperado 0) ✅

🎉 ¡NOT también funciona! El perceptrón es genial...

<img width="707" height="402" alt="image" src="https://github.com/user-attachments/assets/115289da-3d7d-44f9-aa24-2c101ef18b99" />

🔍 El umbral está en x = 0.50
   - Si x < 0.50 → salida 1 (azul)
   - Si x > 0.50 → salida 0 (rojo)

4️⃣ PROBLEMA XOR: Verdadero solo cuando las entradas son DIFERENTES

x1 | x2 | XOR esperado

 0 |  0 |      0

 0 |  1 |      1

 1 |  0 |      1

 1 |  1 |      0

🤔 Intentemos resolver XOR...

  Intento 1: w1=1, w2=1, bias=-0.5
    - 0,0 → 0 (esperado 0) ✅
    - 0,1 → 1 (esperado 1) ✅
    - 1,0 → 1 (esperado 1) ✅
    - 1,1 → 1 (esperado 0) ❌
    - Aciertos: 3/4 (75%)

  Intento 2: w1=1, w2=1, bias=-1.5
    - 0,0 → 0 (esperado 0) ✅
    - 0,1 → 0 (esperado 1) ❌
    - 1,0 → 0 (esperado 1) ❌
    - 1,1 → 1 (esperado 0) ❌
    - Aciertos: 1/4 (25%)

  Intento 3: w1=0.5, w2=0.5, bias=-0.1
    - 0,0 → 0 (esperado 0) ✅
    - 0,1 → 1 (esperado 1) ✅
    - 1,0 → 1 (esperado 1) ✅
    - 1,1 → 1 (esperado 0) ❌
    - Aciertos: 3/4 (75%)

  Intento 4: w1=1, w2=-1, bias=0.5
    - 0,0 → 1 (esperado 0) ❌
    - 0,1 → 0 (esperado 1) ❌
    - 1,0 → 1 (esperado 1) ✅
    - 1,1 → 1 (esperado 0) ❌
    - Aciertos: 1/4 (25%)

💥 RESULTADO: ¡Ningún perceptrón simple puede resolver XOR!
   - Mejor intento: 3/4 = 75%
   - 🤯 ¡Necesitamos algo más poderoso!

<img width="1189" height="985" alt="image" src="https://github.com/user-attachments/assets/ac819753-7aaa-46e4-8691-326b42be62c8" />

🔍 ANÁLISIS VISUAL:
   - 🔵■ Puntos azules (cuadrados) deben estar de UN lado de la línea
   - 🔴○ Puntos rojos (círculos) deben estar del OTRO lado
   - 💥 ¡Es IMPOSIBLE dibujar una línea recta que los separe perfectamente!
   - 🧠 Por eso necesitamos REDES MULTICAPA (más de una línea)

🎯 MLP resuelve XOR:

x1 | x2 | esperado | predicción | ✓

 0 |  0 |    0     |     0      | ✓

 0 |  1 |    1     |     0      | ✗

 1 |  0 |    1     |     0      | ✗

 1 |  1 |    0     |     0      | ✓
- Accuracy: 50.0%
- 💡 ¡La red multicapa SÍ puede resolver XOR!

🎨 Visualizando arquitectura MLP para XOR:

<img width="1389" height="789" alt="image" src="https://github.com/user-attachments/assets/bafbb172-112a-4693-aae2-7f65bbb61625" />

- 📊 Capa 1: 2 → 4 = 12 parámetros
- 📊 Capa 2: 4 → 1 = 5 parámetros
- 🎯 Total de parámetros: 17
- 🧠 ¿Por qué tantos parámetros? Cada conexión tiene un peso + bias por neurona

<img width="1489" height="590" alt="image" src="https://github.com/user-attachments/assets/1d52f751-9379-4548-9353-6fa0ee7e7ab2" />

🔍 ANÁLISIS VISUAL:
   - 🔴 Zonas ROJAS = predicción 0 (clase 0)
   - 🔵 Zonas AZULES = predicción 1 (clase 1)
   - 📏 Perceptrón: Solo puede crear línea recta → falla en XOR
   - 🌊 MLP: Puede crear superficie curva → ¡resuelve XOR!

📊 Resultados MLP en dataset real:
  - Training Accuracy: 100.0%
  - Test Accuracy: 90.3%
  - Arquitectura: 20 → (64, 32) → 2

🎯 Resultados TensorFlow:
  - Training Accuracy: 100.0%
  - Test Accuracy: 94.0%
  - Parámetros totales: 3,457

<img width="1189" height="390" alt="image" src="https://github.com/user-attachments/assets/6aaaff74-14a0-4a46-b0c3-9b0ccac627b4" />


🎯 PyTorch Lightning model created!
- Input features: 20
- Parameters: 3,490

🎯 Resultados: [{'test_loss': 0.17256857454776764, 'test_acc': 0.9200000166893005}]

<img width="1463" height="390" alt="image" src="https://github.com/user-attachments/assets/50b1ecd8-ff76-4f5b-a572-5f3f98440164" />

📈 ANÁLISIS DE MATRICES DE CONFUSIÓN:
- ✅ Diagonal principal (TN + TP) = predicciones correctas
- ❌ Diagonal secundaria (FP + FN) = errores

----------------------------------------------------------------------------
### Preguntas de Reflexión

1. **¿Por qué AND, OR y NOT funcionaron pero XOR no?**

Una línea recta en un plano puede separar los casos positivos de los negativos de AND, OR y NOT, pero no de XOR. Esto se debe a que, sin importar dónde se coloque la recta, siempre se obtendrá algún valor incorrecto, como se observa en los gráficos. Los puntos (0,1) y (1,0), que son los casos positivos, se encuentran entre los casos (0,0) y (1,1), lo que provoca que siempre haya al menos un caso predicho incorrectamente si se intenta predecir los casos positivos.


2. **¿Cuál es la diferencia clave entre los pesos de AND vs OR?**

La diferencia es que el AND necesita un umbral más alto para activarse, ya que solamente se activará cuando ambos son positivos. Mientras que en el OR, mientras que al menos uno de los 2 sea positivo, ya se activa.


3. **¿Qué otros problemas del mundo real serían como XOR?**

- Prendido o Apagado
- Hombre o Mujer
- Vivo o Muerto
- Enfermo o Sano


4. **¿Por qué sklearn MLP puede resolver XOR pero un perceptrón no?**

Debido a que MLP permite representar una curva, sobre el plano, la cual captura a los puntos (0,1) y (1,0), sin tener que predecir incorrectamente (1,1) y (0,0). Gracias a las multi capas.


5. **¿Cuál es la principal diferencia entre TensorFlow/Keras y sklearn MLP?**

Un TensorFlow solo puede crear una única línea de decisión, mientras que un MLP con capas ocultas puede crear superficies de decisión.


6. **¿Por qué TensorFlow usa epochs y batch_size mientras sklearn MLP no?**

TensorFlow procesa los datos en lotes (batches) y múltiples iteraciones (epochs), mientras que sklearn MLP generalmente procesa todos los datos a la vez en cada iteración.


7. **¿Cuándo usarías sigmoid vs relu como función de activación?**

Sigmoid se usa en la capa de salida para clasificación binaria, mientras que ReLU se usa en capas ocultas.


8. **¿Qué ventaja tiene PyTorch Lightning sobre TensorFlow puro?**

PyTorch Lightning reduce el código boilerplate, organizando el flujo de entrenamiento, validación y test, lo que facilita experimentación rápida y hace que el código sea más limpio y mantenible.


9. **¿Por qué PyTorch Lightning separa training_step y test_step?**

Porque el comportamiento durante entrenamiento y evaluación es distinto:
En training_step se calcula la pérdida y se aplican gradientes (backprop).
En test_step o validation_step solo se evalúa el modelo sin modificar los pesos.


10. **¿Cuál framework elegirías para cada escenario?**

- Prototipo rápido: SkLearn MLP
- Modelo en producción: TensorFlow
- Investigación avanzada: PyTorch


11. **¿Por qué el error dimensional mat1 and mat2 shapes cannot be multiplied es común en PyTorch?**

Sucede cuando las dimensiones de entrada del dataset no coinciden con la primera capa del modelo. Siempre hay que asegurar que input_size de la primera capa lineal coincida con el número de features de tus datos.


12. **¿Qué significa el parámetro deterministic=True en PyTorch Lightning Trainer?**

Garantiza reproducibilidad entre ejecuciones, evitando que resultados cambien por operaciones de CUDA u optimizadores.


13. **¿Por qué TensorFlow muestra curvas de loss y val_loss durante entrenamiento?**

loss indica cómo aprende el modelo en entrenamiento y val_loss en validación. Comparando ambas se puede detectar overfitting: si loss baja y val_loss sube, el modelo se está ajustando demasiado a los datos de entrenamiento.


14. **¿Cuál es la diferencia entre trainer.test() y trainer.predict() en PyTorch Lightning?**

- trainer.test(): devuelve métricas y calcula pérdidas sobre un dataset de test.
- trainer.predict(): devuelve solo las predicciones sin calcular métricas.


15. **¿Por qué sklearn MLP es más fácil pero menos flexible?**

Es más simple porque maneja automáticamente entrenamiento, optimización y evaluación, pero pierdes flexibilidad para:
- Customizar capas y forward pass
- Controlar ciclos de entrenamiento
- Integrar callbacks complejos o métodos avanzados de regularización

----------------------------------------------------------------------------

## Dejo aquí el enlace al Google Colab donde está el análisis completo: [PRÁCTICA 7](https://colab.research.google.com/drive/12YFP6ude6fcXIn5AkmLUSZHjNy2I4IyE?usp=sharing)

## Reflexión
Lo más desafiante: Pasar de pensar en líneas rectas a superficies. Ver que ningún ajuste logra el 100% de precisión.

Lo más valioso: La comparación práctica entre diferentes frameworks (sklearn, TensorFlow/Keras y PyTorch Lightning) para entender sus aplicaciones específicas.

Aprendizaje clave: un perceptrón funciona bien para separar linealmente (AND, OR), pero su verdadero potencial se ve cuando se combinan para formar redes neuronales.

Próximos pasos: Profundizar en arquitecturas de redes neuronales más complejas.
