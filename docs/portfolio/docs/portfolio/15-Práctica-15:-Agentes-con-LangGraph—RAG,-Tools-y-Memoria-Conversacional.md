---
title: "Entrada 15 — Agentes con LangGraph — RAG, Tools y Memoria Conversacional"
date: 2025-11-18
---

# 👮‍♀️ Agentes con LangGraph: Construyendo Asistentes con Memoria y RAG

## Contexto
Implementación de un agente inteligente utilizando LangGraph, combinando herramientas de RAG, consulta de estado del sistema y memoria conversacional en un grafo de estado ejecutable.

## Objetivos
- Crear un grafo de estado con LangGraph para orquestar un agente conversacional
- Integrar herramientas de RAG para búsqueda en base de conocimiento
- Implementar memoria ligera mediante resúmenes conversacionales
- Desarrollar una interfaz interactiva con Gradio para probar el agente

## Actividades (con tiempos estimados)
1. Setup inicial y Hello Agent (15 min)
2. Definición del estado del agente con memoria ligera (20 min)
3. Construcción del sistema RAG mínimo (25 min)
4. Implementación de tools adicionales (15 min)
5. Integración de tool calling con LLM (30 min)
6. Desarrollo del grafo completo assistant ↔ tools (25 min)
7. Pruebas multi-turn y memoria (20 min)
8. Interfaz Gradio (15 min)

## Desarrollo
Se construyó un agente completo que combina capacidades de reasoning con herramientas específicas. El sistema utiliza:
- Grafo de estado: Nodos para assistant, tools y memory
- RAG personalizado: Base de conocimiento con información de la empresa
- Tools integradas: Búsqueda semántica y consulta de estado del sistema
- Memoria conversacional: Resúmenes periódicos para mantener contexto
- Interfaz interactiva: Chatbot con Gradio para pruebas en tiempo real

## Evidencias
- ¿Qué diferencia hay entre esto y hacer llm.invoke("prompt") directo?  La diferencia es que con LangGraph no le estás tirando un prompt suelto al modelo: estás moviendo un estado que va pasando de nodo en nodo. Cada nodo agarra ese estado, lo modifica y lo vuelve a pasar. En cambio, cuando hacés llm.invoke("prompt"), no hay recorrido, no hay memoria ni pasos: solo mandás texto y recibís texto
- ¿Dónde ves explícitamente que hay un estado que viaja por el grafo? Se ve explicitamente cuando:
  - Lo definís como AgentState.
  - Lo pasás al grafo con graph.invoke(initial_state).
  - Cada nodo lo recibe como state en def assistant_node(state).

- ¿Qué ventaja tiene guardar un summary en vez de todo el historial? Guardar un resumen en lugar de todo el historial hace que el agente sea más rápido y eficiente, porque no necesita procesar cada mensaje cada vez. Además, permite concentrarse en lo importante y mantener el contexto de la conversación sin todo el ruido de los mensajes antiguos, haciendo que la charla sea más clara y fluida.
- ¿Qué información NO deberías guardar en ese resumen por temas de privacidad? Por motivos de privacidad, nunca se debe incluir datos sensibles de las personas, como nombres completos, direcciones, contraseñas o información financiera. El resumen debe ser útil para el agente y seguro, solo con lo necesario para continuar la conversación.

- ¿Qué cambiarías si el corpus fuera mucho más grande? Si el corpus fuera mucho más grande, habría que pensar en estrategias para no sobrecargar al modelo ni la búsqueda, probablemente debería usar un índice más eficiente, limitaría la cantidad de resultados o resumiría los documentos antes de pasarlos como contexto.
- ¿Qué pasaría si devolvés textos muy largos en el context? Devolver textos demasiado largos también puede ser un problema, porque el LLM tiene un límite de tokens y puede perder foco en lo importante, además, se vuelve más lento y caro procesar tanta información. Por eso conviene que la tool entregue solo lo relevante y conciso para que el agente pueda usarlo efectivamente.

- ¿Qué problema tendría esta tool si la usás en producción real? Si la usáramos en producción real, estas tools tendrían varios problemas: por un lado, FAKE_ORDERS es solo un diccionario en memoria, así que no refleja datos reales ni concurrentes, y cualquier acceso simultáneo podría generar inconsistencias. Además, no hay validación ni control de errores sofisticado, y exponer directamente funciones como get_order_status o get_utc_time podría abrir vulnerabilidades si se reciben inputs maliciosos.
- ¿Cómo la harías más segura / robusta? Para hacerlas más seguras y robustas habría que conectarlas a una base de datos real con control de acceso, validar y sanear los inputs, manejar errores de manera confiable, y limitar la información sensible que se devuelve, asegurando que solo se entregue lo necesario para cada usuario.

- ¿Dónde está ahora el “reasoning”? ¿En qué nodo? El reasoning ahora ocurre principalmente en el nodo assistant. Es ahí donde el LLM analiza el historial de mensajes y decide si puede responder directamente o si necesita llamar a alguna tool. El nodo de tools simplemente ejecuta lo que se le pide; no decide ni razona por sí mismo.
- ¿Cómo cambiaría el diseño si tuvieras 10 tools en vez de 2-3? Si tuvieras 10 tools en lugar de 2 o 3, el diseño debería ser más organizado: probablemente convendría tener un sistema de routing más sofisticado para decidir cuál tool llamar, o categorizar las tools por tipo de tarea para no sobrecargar al LLM con demasiadas opciones a la vez. Esto ayudaría a mantener eficiente la toma de decisiones y evitar confusiones en la elección de herramientas.

### Respuesta 1: 
LangGraph es una plataforma/SDK para diseñar, ejecutar y monitorizar aplicaciones basadas en modelos de lenguaje mediante grafos de componentes. Permite componer pasos (prompts, llamadas a LLMs, embeddings, búsquedas en vectores, herramientas externas) de forma visual o por código, gestionar versiones, hacer pruebas y observar el comportamiento en producción. En pocas palabras: facilita construir y coordinar pipelines de IA conversacional/LLM sin tener que ensamblar todo desde cero.

¿Quieres que te muestre un ejemplo rápido o cómo sería un pequeño flujo?

### Respuesta 2: 
RAG = Retrieval-Augmented Generation. En pocas palabras: es una técnica que combina un sistema de recuperación (search/recall) con un generador de lenguaje (LLM) para que las respuestas se apoyen en documentos reales en lugar de solo en la memoria del modelo.

Cómo funciona (resumen):
- Se recibe la consulta del usuario.
- Un retriever (BM25 o retriever denso con embeddings) busca documentos relevantes en una colección o vector DB.
- Se toman las top‑k evidencias y se pasan al generador (un LLM) junto con la consulta.
- El LLM produce la respuesta condicionada en esas evidencias (y la consulta), lo que ayuda a fundamentar la salida.

Componentes típicos:
- Índice/colección de documentos (base de conocimiento).
- Retriever (sparse o dense; a menudo embeddings + ANN).
- Reranker opcional.
- Generador/decoder (seq2seq LLM).
- Orquestación y lógica de fusión/aggregate (p. ej. RAG‑Sequence, RAG‑Token, o enfoques como Fusion‑in‑Decoder).

Ventajas:
- Reduce hallucinations al basar respuestas en evidencia externa.
- Permite respuestas con información actualizable sin reentrenar el modelo.
- Escalable para grandes colecciones.

Limitaciones y retos:
- Calidad depende de la recuperación (si no recupera la evidencia correcta, la respuesta puede ser errónea).
- Latencia y coste mayores (búsqueda + generación).
- Requiere gestión de índices, filtrado y control de versiones de datos.
- Aun puede “alucinar” combinando mal las evidencias o extrapolando.

Usos comunes:
- Sistemas de preguntas y respuestas sobre documentación/FAQ.
- Asistentes con acceso a bases de conocimiento internas o datos actualizados.
- Soporte técnico, legal, médico (con cuidado y validación).

Si querés, te muestro un ejemplo corto en Python (LangChain/FAISS) o un diagrama del flujo. ¿Cuál preferís?

### Respuesta 3
Último mensaje: human → Usá tu base de conocimiento y decime qué es RAG.
Último mensaje: ai → RAG = Retrieval-Augmented Generation. En pocas palabras: es una técnica que combina búsqueda (recuperación) de información relevante en una base de conocimientos con generación de texto por un modelo de lenguaje, para que las respuestas estén fundamentadas en documentos y no solo en la memoria del modelo.

Concepto y por qué se usa
- Problema: los LLMs pueden olvidar hechos recientes o inventar (hallucinar) respuestas.
- Solución RAG: antes de generar la respuesta, buscar fragmentos relevantes en una colección (docs, FAQ, base interna, web), y dar esos fragmentos como contexto al modelo para que los use al generar la salida.

Componentes básicos
1. Indexación: preparar y almacenar documentos (texto, PDFs, bases) en una estructura indexable.
2. Representación: convertir documentos y consultas a vectores (embeddings) o usar índices invertidos (BM25).
3. Recuperador (retriever): dado el input del usuario, devuelve los documentos o pasajes más relevantes.
4. Re-ranker (opcional): ordena o filtra los resultados recuperados para mayor precisión.
5. Generador: un LLM que recibe la consulta y los pasajes recuperados (en el prompt) y genera la respuesta final.
6. Post-procesado: citar fuentes, limitar la longitud, verificar con reglas, etc.

Tipos de retrieval
- Sparse retrieval: búsquedas por términos (BM25).
- Dense retrieval: búsqueda por similitud de embeddings (FAISS, Milvus).
- Híbrido: combina ambos para mejor cobertura.

Ventajas
- Respuestas más precisas y actualizables sin reentrenar el modelo.
- Permite auditar y citar fuentes.
- Maneja conocimiento específico de dominio o reciente.

Limitaciones y riesgos
- Calidad depende de la indexación y de la capacidad del retriever.
- Latencia mayor (recuperación + generación).
- Si los pasajes contienen errores, el modelo puede propagar o mezclar información incorrecta.
- Manejo de contexto limitado por el tamaño del prompt; hay que seleccionar bien los pasajes.

Buenas prácticas
- Limitar y seleccionar pasajes relevantes (chunking y scoring).
- Incluir instrucciones en el prompt para usar o citar solo la información recuperada.
- Re-rankeado y verificación de hechos cuando importa la exactitud.
- Actualizar el índice para mantener datos recientes.

Casos de uso
- Asistentes de atención al cliente con base de conocimientos.
- Sistemas de preguntas y respuestas sobre documentación técnica.
- Chatbots legales/medicina (con verificación y control humano).
- Resúmenes y búsqueda semántica en grandes colecciones.

Si querés, te muestro un flujo simple paso a paso o un ejemplo de prompt/arquitectura con herramientas comunes (FAISS, embeddings, LLM). ¿Querés eso?


- ¿Reconocés cuándo el agente está llamando rag_search vs get_order_status? Se puede ver claramente cuándo el agente está llamando a rag_search o a get_order_status porque el LLM genera una tool call en su mensaje. Esa llamada indica que no está respondiendo directamente, sino que necesita ejecutar una herramienta para obtener información.
- ¿Qué tipo de prompts le darías al modelo para que use tools “con criterio”? Para que el modelo use las tools con criterio, conviene darle prompts claros que expliquen qué hace cada tool, cuándo conviene usarla y qué tipo de respuesta se espera. De esta manera, el LLM puede decidir de forma más inteligente si necesita recurrir a una tool o si puede responder directamente con lo que ya sabe.

- ¿Cómo decidirías cada cuánto actualizar el summary? Actualizaría el summary cada cierto número de turnos o cuando la conversación haya cambiado de tema de manera significativa, de modo que refleje el contexto relevante sin ser redundante ni demasiado frecuente.
- ¿Qué tipo de info deberías excluir del summary? En el resumen no incluiría información sensible o privada de los usuarios, como datos personales, contraseñas o detalles financieros; solo debería concentrarse en lo importante para que el agente recuerde el hilo de la conversación y pueda dar respuestas coherentes.

<img width="1919" height="858" alt="image" src="https://github.com/user-attachments/assets/beae42e0-c078-4a7e-b297-e91b4b55fa21" />

### Mini-agente de Soporte con RAG + Tool de Estado
<img width="1919" height="861" alt="image" src="https://github.com/user-attachments/assets/184ce80d-d115-454c-9693-7315753ef39b" />


## Dejo aquí el enlace al Google Colab donde está el análisis completo: [PRÁCTICA 15](https://colab.research.google.com/drive/1lyYC0JWZxmRKrGqxBWT21f-fCmAGBspF?usp=sharing)

## Reflexión
Lo más desafiante: Entender el flujo del grafo de estado, especialmente la gestión del estado.

Lo más valioso: Ver cómo el agente decide automáticamente cuándo usar tools vs responder directo, demostrando reasoning práctico.

Aprendizaje clave: En lugar de un solo prompt, donde tengo que incluir manualmente todo el historial de la conversación si quiero hacer un seguimiento, creas un grafo con diferentes nodos. Cada nodo es un paso especializado en un proceso.

Próximos pasos: Explorar arquitecturas más complejas con múltiples agentes.
