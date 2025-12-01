---
title: "Entrada 14 — Práctica 14: LLMs con LangChain (OpenAI) — Prompting, Plantillas y Salida Estructurada (ES)"
date: 2025-11-11
---

# ⚙️ Configuración y Parámetros de LLMs con LangChain

## Contexto
Configuración inicial de un entorno para trabajar con modelos de lenguaje (LLMs) utilizando LangChain, explorando parámetros clave como temperature, top_p y max_tokens, y aplicando plantillas estructuradas con ChatPromptTemplate y LCEL.

## Objetivos
- Configurar el entorno LangChain y conectarse a modelos OpenAI.
- Experimentar con parámetros de generación de texto (temperature, top_p).
- Utilizar ChatPromptTemplate para crear prompts reutilizables.
- Introducir el uso de LangSmith para monitoreo y métricas.

## Actividades (con tiempos estimados)
1. Setup inicial y Hello LLM (15 min): Instalación de librerías y primera interacción con un LLM.
2. Parámetros clave (30 min): Experimentación con temperature, max_tokens y top_p.
3. Plantillas con ChatPromptTemplate + LCEL (20 min): Creación de cadenas de procesamiento con prompts estructurados.
4. Métricas mínimas con LangSmith (10 min): Configuración de trazas para monitorear ejecuciones.

## Desarrollo
Se configuró el entorno con las librerías necesarias y claves de API. La exploración de parámetros como temperature (0.0, 0.5, 0.9) reveló que valores bajos generan respuestas deterministas, mientras que valores altos permiten mayor creatividad. Se implementaron plantillas reutilizables con ChatPromptTemplate que mejoraron la mantenibilidad del código, y se configuró LangSmith para monitorear métricas como tokens y latencia.

## Evidencias

**Temp = 0.2:**
- ¿Qué cambia si pedís 1 vs 3 oraciones?

**Resultados:**

"Soy ChatGPT, un modelo de la familia GPT-4 (versión GPT-4o)."

"Soy ChatGPT, un modelo de lenguaje con corte de conocimiento en junio de 2024."

"Soy ChatGPT, un modelo de lenguaje de OpenAI con conocimiento actualizado hasta junio de 2024."

- ¿Observás variancia entre ejecuciones con la misma consigna?

Hay algo de variancia, aunque pequeña. Por ejemplo, todas comienzan con la frase "Soy ChatGPT, un modelo de", y luego las últimas dos mencionan la misma información sobre la fecha del conocimiento.

**Temp = 0.9:**
- ¿Qué cambia si pedís 1 vs 3 oraciones?

**Resultados:**

"Soy ChatGPT, un modelo de lenguaje de OpenAI; la versión exacta no está especificada en este entorno."

"Soy ChatGPT (modelo GPT-4o), con corte de conocimiento en junio de 2024."

"Soy ChatGPT, modelo GPT-4o (corte de conocimiento: junio de 2024)."

- ¿Observás variancia entre ejecuciones con la misma consigna?

Podemos observar que la primera respuesta se contradice con las otras, que sí indican una versión. Aun así, podemos ver cierta similitud, sobre todo en las últimas dos respuestas, y todas empiezan por "Soy ChatGPT". Diría que la variancia es mayor que en el primer caso.


--- Temperature=0.0 ---
[1] Celebrando este paper de IA: innovación, rigor y ética que transforman el futuro. ¡Bravo equipo!
[2] - Capturan dependencias a largo plazo con mecanismos de atención sin procesar secuencialmente, evitando problemas de desvanecimiento/explosión del gradiente.  
- Permiten paralelización masiva en entrenamiento (GPU/TPU), acelerando convergencia respecto a RNNs.  
- Ofrecen alto rendimiento y transferibilidad: preentrenamiento + fine‑tuning funciona en múltiples tareas y dominios (NLP, visión, audio).

--- Temperature=0.5 ---
[1] ¡Gran paper! Impulsa la IA hacia soluciones responsables e innovadoras. Felicitaciones al equipo investigador.
[2] - Manejo efectivo de dependencias a largo plazo gracias a la atención (self-attention) sin recurrencia.  
- Alta paralelización en entrenamiento (operaciones matriciales), lo que acelera el aprendizaje en hardware moderno.  
- Gran escalabilidad y transferibilidad: modelos preentrenados se adaptan bien a muchas tareas y modalidades.

--- Temperature=0.9 ---
[1] Brillante artículo de IA: innovación, rigor y impacto real. ¡Enhorabuena al equipo!
[2] - Capturan dependencias a larga distancia mediante self-attention, sin procesar secuencialmente los tokens.  
- Facilitan entrenamiento altamente paralelo y escalado a modelos y datos grandes (eficiencia en GPUs/TPUs).  
- Muy versátiles: funcionan en texto, audio e imagen y permiten preentrenamiento + fine-tuning transferible a muchas tareas.

**Resultados**

**Temp 0.0 y top_p = 1.0**

Métrica y test,  
cruces, sesgo y ruido,  
entrega verdad.

¿Querés otra versión (más técnica o más lírica)?

---

**Temp 0.5 y top_p = 0.9**

Datos en la mesa,  
métricas que susurran,  
verdad y ruido.

---

**Temp 0.9 y top_p = 0.7**

Datos en la red,  
métricas que revelan,  
modelo en su ser.

---

**¿Qué combinación te da claridad vs creatividad?**  
- Para la claridad la mejor combinación fue **Temp 0.0 + top_p 1.0**, porque genera un haiku más preciso, directo y consistente entre ejecuciones. El contenido es más “fijo”.  **Temp 0.5 + top_p 0.9** es donde aparece algo de variación pero sin perder coherencia. Y **Temp 0.9 + top_p 0.7** produce frases más libres, y asociaciones menos literales.

**¿Cómo impactan estos parámetros en tareas “cerradas” (respuestas únicas)?**  
- Temperature bajo (0.0–0.2): ideal para tareas cerradas porque reduce la variabilidad y aumenta la precisión.
- Temperature medio (0.5): funciona, pero puede introducir ligera variación y riesgos de desviarse del objetivo.  
- Temperature alto (0.9): puede inventar detalles, desviarse del formato o perder exactitud, por lo que no seria bueno en tareas cerradas.  
- top_p bajo (0.7): restringe el espacio de palabras, meora las tareas cerradas por mantener coherencia.  
- top_p alto (1.0): deja más libertad, pero no se debe combinar con temperatura alta. No es recomendable para respuestas únicas.


- ¿Qué mejora frente a “parsear a mano” cadenas JSON?

Usar salidas estructuradas evita errores comunes del parseo manual y garantiza que el formato sea siempre válido. Y reduce la complejidad del código.

- ¿Qué contratos de salida necesitás en producción?

Se requieren respuestas con estructura estable, tipos definidos y campos obligatorios claros. Permite validar fácilmente la salida y asegurar una consistencia, evitando cambios inesperados.


<img width="861" height="304" alt="image" src="https://github.com/user-attachments/assets/4a067c96-0cad-43dd-b579-023b4259eefb" />

<img width="879" height="278" alt="image" src="https://github.com/user-attachments/assets/daae0105-cd01-4286-92fe-99225161154c" />

<img width="883" height="277" alt="image" src="https://github.com/user-attachments/assets/6c8a20bc-a06a-40e8-acdc-e27417ab2b26" />

- ¿Qué prompt te costó más tokens?

Los prompts más extensos son los que más tokens costaron; en este caso, fue el último, sobre Transformers vs RNNs.

- ¿Cómo balancear latencia vs calidad?

Usar prompts más cortos, evitar contexto innecesario, utilizar modelos más rápidos para tareas simples y reservar los modelos grandes solo para tareas que realmente requieren mayor calidad.

Resumen ejecutivo generado por el modelo:

Intro: La creciente dependencia de la inteligencia artificial en las organizaciones modernas trae beneficios, pero también riesgos significativos. 

Hallazgos: Se identifican problemas de transparencia, sesgos en los modelos y deficiencias en la calidad de datos. Además, muchas empresas carecen de marcos de gobernanza adecuados para monitorear y auditar estos sistemas.

Recomendación: Es crucial implementar prácticas robustas de evaluación, auditoría continua y control del ciclo de vida de los modelos para maximizar el potencial de la IA, garantizando seguridad y confiabilidad.
content='La ventaja del structured output es que permite una interpretación y procesamiento más fácil y eficiente de los datos, facilitando la integración con otros sistemas y la automatización de tareas.' additional_kwargs={'refusal': None} response_metadata={'token_usage': {'completion_tokens': 34, 'prompt_tokens': 55, 'total_tokens': 89, 'completion_tokens_details': {'accepted_prediction_tokens': 0, 'audio_tokens': 0, 'reasoning_tokens': 0, 'rejected_prediction_tokens': 0}, 'prompt_tokens_details': {'audio_tokens': 0, 'cached_tokens': 0}}, 'model_provider': 'openai', 'model_name': 'gpt-4o-mini-2024-07-18', 'system_fingerprint': 'fp_2b91e6dc70', 'id': 'chatcmpl-Chh8ZMPBwIgiR6eI4WruFXpOlAxYU', 'service_tier': 'default', 'finish_reason': 'stop', 'logprobs': None} id='lc_run--dad0ff9c-fa6b-4280-a722-89f61e120fab-0' usage_metadata={'input_tokens': 55, 'output_tokens': 34, 'total_tokens': 89, 'input_token_details': {'audio': 0, 'cache_read': 0}, 'output_token_details': {'audio': 0, 'reasoning': 0}}

- ¿Cuándo “alucina” el modelo al no tener suficiente contexto?

El modelo alucina cuando la información necesaria no está en el contexto y no se le da una instrucción clara para admitirlo. En este caso, gracias al prompt estricto "Respondé SOLO usando el contexto", no alucinó.

- ¿Cómo exigir formato y concisión de manera consistente?

Usando structured_output para obligar al JSON, mensajes system que definan el formato exacto, límites de longitud y prompts con estructura fija. Reduce variabilidad y garantiza respuestas consistentes.

== Zero-shot ==
POS
NEG
NEU

== Few-shot ==
Etiqueta: POS
NEG
POS

- ¿Mejora la consistencia al ajustar el número/elección de ejemplos?

Sí. Agregar 1-2 ejemplos en el few-shot mejora la consistencia de la clasificación.
Con zero-shot, el modelo puede dudar con frases ambiguas "Está bien, nada extraordinario", pero con ejemplos cercanos, tiende a etiquetar siempre de forma más estable, ej: NEU. Además, la elección de ejemplos importa: si incluís ejemplos más variados, el modelo generaliza mejor.

- Impacto de cambiar la temperatura

Temp baja: clasificación estable, siempre repite el mismo criterio.
Temp alta: más variabilidad, a veces cambia NEU por POS

=== RESUMEN DIRECTO ===

La metamorfosis, novela de Franz Kafka publicada en 1915, narra la transformación de Gregorio Samsa en un insecto y el drama familiar que ello provoca. Su título original en alemán, Die Verwandlung, podría traducirse como "La transformación", aunque en español se la conoce como La metamorfosis, con connotaciones míticas. La obra suele interpretarse como una alegoría del enfrentamiento del individuo con un mundo moderno opresor y es considerada una pieza clave en la literatura del absurdo que influyó a numerosos autores posteriores.

=== RESUMEN MAP-REDUCE ===

La Metamorfosis (Die Verwandlung), novela de Franz Kafka publicada en 1915, narra la súbita transformación de Gregorio Samsa en un insecto y el drama familiar que provoca. El título alemán —«la transformación»— se tradujo como Metamorfosis, con matiz mítico. La obra funciona como alegoría del individuo frente a un mundo moderno opresivo, inaugura la literatura del absurdo e influyó en autores posteriores.

- Compará “resumen directo” (sin split) vs map-reduce.

En la prueba, el resumen directo salió bien pero un poco más largo y con alguna repetición. El map-reduce, en cambio, quedó más compacto y parejo, como si estuviera mejor editado.
En este texto corto no hubo una diferencia enorme, pero se nota que map-reduce ayuda a ordenar y limpiar las ideas. En textos largos seguramente la ventaja sería mucho mayor.

- ¿Cómo afectan chunk_size y chunk_overlap la calidad?

El chunk_size influye en cuánto contexto ve el modelo: si es muy chico pierde ideas, si es muy grande se parece demasiado al texto original y no aporta mucho.

El chunk_overlap ayuda a que no se corten frases o ideas entre chunks: poco overlap pierde continuidad, demasiado genera repeticiones.

=== Resultado 1 (básico) ===
titulo=None fecha='05/11/2025' entidades=[Entidad(tipo='Organización', valor='OpenAI'), Entidad(tipo='Organización', valor='Universidad Católica del Uruguay'), Entidad(tipo='Ubicación', valor='Montevideo')]

=== Resultado 2 (fecha ambigua) ===
titulo=None fecha='03/04/25' entidades=[Entidad(tipo='Organización', valor='IBM'), Entidad(tipo='Institución pública', valor='Intendencia de Canelones')]

=== Resultado 3 (sin fecha) ===
titulo='Amazon abrirá un nuevo centro de investigación en Río de Janeiro.' fecha=None entidades=[Entidad(tipo='Organización', valor='Amazon'), Entidad(tipo='Instalación', valor='centro de investigación'), Entidad(tipo='Ubicación', valor='Río de Janeiro')]

El modelo identifica bien organizaciones y ubicaciones. En los tres casos capturó entidades relevantes sin errores graves.

Tuvo problemas con categorías inconsistentes, usa etiquetas distintas para conceptos similares "Organización", "Institución pública", "Instalación".

Si no se fija un conjunto de tipos permitido, el modelo inventa variaciones.

Las fechas ambiguas se devuelven tal cual, no intenta inferir si 03/04/25 es 3 de abril o 4 de marzo.
El modelo no desambigua fechas por sí mismo si no se lo pedís explícitamente.

Cuando no hay fecha, completa el campo con None según el esquema, lo que demuestra que maneja bien campos opcionales.

=== FAISS | k=2 | Prompt estricto ===
Aporta mejor grounding: al combinar recuperación y generación, y usando la recuperación para evitar alucinaciones del modelo.

=== FAISS | k=4 | Prompt estricto ===
La ventaja clave es que RAG combina recuperación y generación para mejorar el grounding del modelo, siendo la recuperación fundamental para evitar alucinaciones.

=== Chroma | k=2 | Prompt flexible ===
La ventaja clave de RAG es que mejora el grounding del modelo al combinar recuperación y generación: la etapa de recuperación aporta evidencia factual que reduce las alucinaciones y aumenta la fidelidad de las respuestas.

Adicionalmente (inferido):
- Permite acceder a conocimiento externo y más actualizado, porque recupera documentos fuera del modelo.
- Mejora la trazabilidad/falsabilidad: es más fácil verificar y citar las fuentes usadas por la generación.

(Lo principal viene del contexto; las dos últimas ventajas las he inferido.)

=== Chroma | k=4 | Prompt flexible ===
La ventaja clave de RAG (según el contexto) es que permite groundear las respuestas del modelo recuperando documentos relevantes antes de generar texto, lo que reduce las alucinaciones y mejora la exactitud factual.

Apoyo técnico (contexto):
- La etapa de recuperación es decisiva para evitar alucinaciones.
- OpenAIEmbeddings sirve para convertir textos en vectores y así indexarlos para la búsqueda.
- LangChain puede ayudar a producir salidas estructuradas y controladas (por ejemplo con Pydantic).

Inferencia (aclaración): además, RAG facilita la trazabilidad y la actualización del conocimiento sin reentrenar el modelo, porque basta con actualizar el índice de documentos.

1. k más alto (k=4) no cambia demasiado el contenido, pero sí hace que la respuesta sea más completa y repetida.
El modelo recibió más contexto y por eso reforzó la misma idea "mejor grounding", pero no agregó nada realmente nuevo.

2. k más bajo (k=2) sigue dando buenas respuestas.
Con poca información relevante ya puede contestar correctamente, puede que el conjunto de documentos sea chico y muy directo.

3. FAISS y Chroma se comportaron prácticamente igual.
Ambos recuperaron bien. En un dataset chico no hay diferencias prácticas.

4. El prompt flexible permitió inferencias extra.
Como se le dio permiso para inferir, el modelo agregó:

- acceso a conocimiento externo
- trazabilidad
- cosas que no estaban en los documentos, pero son razonables.

Esto confirma que con la regla "infiere", va a inferir.

5. El prompt estricto cumplió: cero inferencias.
Se mantuvo pegado al contexto, lo cual es lo esperado.

### Chatbot de Soporte “FAQ + WebSearch”
<img width="1919" height="859" alt="image" src="https://github.com/user-attachments/assets/f16d8ff5-7dfe-44a6-9555-c53ffc8097fc" />

#### Cómo Funciona

1. **Documentos de Ejemplo**
   - 8 documentos de ejemplo sobre "Producto X" (una herramienta ficticia de gestión de proyectos)
   - Indexados con FAISS usando embeddings de OpenAI
   - Recupera los 3 fragmentos más relevantes para cada consulta

2. **Lógica de Decisión**
   - Si el contexto de las FAQ es suficiente (>50 caracteres), usa solo el conocimiento local (alta confianza)
   - Si las FAQ son insuficientes, activa búsqueda web con DuckDuckGo (confianza media/baja)

3. **Estructura de Respuesta**
   - Usa modelos Pydantic para definir el formato de salida JSON
   - Devuelve: respuesta, fuentes (título + URL), nivel de confianza

4. **Parámetros del Modelo**
   - Modelo: GPT-3.5-turbo (rápido y económico)
   - Temperature: 0.3 (equilibrio entre precisión y creatividad)
   - Recuperación: 3 fragmentos principales de las FAQ

##### Instrucciones de Configuración
- **Ejecutar Todas las Celdas**: Ejecuta el notebook de arriba a abajo
- **Probar**: El script prueba automáticamente 3 preguntas de ejemplo

##### Personalización
- **Agregar más FAQs**: Extiende la lista `faq_documents`
- **Ajustar umbral**: Cambia el umbral de 50 caracteres para activar búsqueda web
- **Modificar salida**: Actualiza el modelo Pydantic `BotResponse`

## Dejo aquí el enlace al Google Colab donde está el análisis completo: [PRÁCTICA 14](https://colab.research.google.com/drive/1MIwekmPWzHJyxlHs5u_SddaeWs-FOpdp?usp=sharing)

## Reflexión
Lo más desafiante: Ajustar los parámetros de generación (temperature, top_p) para diferentes casos de uso.

Lo más valioso: Aprender a estructurar prompts con ChatPromptTemplate y LCEL, facilitando la reutilización y el mantenimiento del código.

Aprendizaje clave: Los parámetros de generación afectan significativamente la calidad y variabilidad de las respuestas, y su elección depende del uso específico.

Próximos pasos: Explorar arquitecturas más complejas con múltiples agentes especializados.
