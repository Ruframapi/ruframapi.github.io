# Notas de Procesamiento de Lenguaje Natural
## De fundamentos clásicos a modelos neuronales y LLMs

### Tópicos que aborda el libro
- Introducción al PLN
- Pipeline y preprocesamiento de texto
- Recuperación de información
- Evaluación de sistemas de IR
- Modelos de lenguaje n-grama
- Clasificación de texto y análisis de sentimientos
- Semántica vectorial e incrustaciones
- Redes feedforward para lenguaje
- RNN y LSTM
- Encoder-decoder y tokenización de subpalabras
- Transformer
- MLM y BERT
- LLMs y fine-tuning eficiente
- Prompting, RAG y alineación
- Ética, riesgos e implicaciones del PLN y los LLMs

### Estructura del contenido
#### Parte I. Fundamentos y técnicas clásicas
1. Introducción al PLN
2. Pipeline y preprocesamiento
3. Recuperación de información
4. Evaluación de IR
5. Modelos n-grama
6. Clasificación de texto
7. Semántica vectorial e incrustaciones

#### Parte II. Modelos neuronales y LLMs
8. Feedforward para lenguaje
9. RNN y LSTM
10. Encoder-decoder y subpalabras
11. Transformer
12. MLM y BERT
13. LLMs y PEFT
14. Prompting, RAG y alineación

#### Parte III. Aspectos éticos y riesgos
15. Ética y riesgos



# Prefacio

Escribir un libro sobre procesamiento del lenguaje natural (PLN) en la actualidad puede parecer una decisión difícil de justificar. La disciplina cuenta con excelentes textos de referencia, entre ellos *Speech and Language Processing* de Jurafsky y Martin, considerado desde hace años la obra canónica del área. Además, vivimos en una época en la que los modelos de inteligencia artificial pueden responder preguntas, generar explicaciones y producir material educativo casi de manera instantánea.

Entonces, ¿por qué escribir otro libro?

La respuesta es sencilla. Este libro no nació con el propósito de reemplazar las obras de referencia existentes ni de competir con las herramientas de inteligencia artificial. Surgió como resultado de una necesidad docente.

Durante más de seis años he impartido un curso introductorio de procesamiento del lenguaje natural para estudiantes de ingeniería. Con el tiempo, las notas de clase fueron creciendo, reorganizándose y refinándose semestre tras semestre. Cada capítulo fue escrito para responder una pregunta específica que surgía en el aula, para explicar un concepto que tradicionalmente resultaba difícil o para establecer una conexión entre ideas que los estudiantes solían aprender de forma fragmentada.

El resultado es el material que el lector tiene ahora en sus manos.

Este libro representa una organización del contenido que ha sido puesta a prueba durante varios años de docencia. No pretende ser una enciclopedia del PLN ni cubrir exhaustivamente todos los temas de investigación. Su objetivo es diferente. Busca ofrecer un recorrido coherente que permita comprender cómo evolucionó el campo, desde los métodos clásicos basados en reglas y estadísticas hasta los modelos neuronales, los transformers y los grandes modelos de lenguaje. Cada capítulo fue concebido como un peldaño sobre el cual construir el siguiente, procurando que las ideas aparezcan en el momento en que resultan más naturales para el proceso de aprendizaje.

Otro aspecto que motivó este proyecto fue la disponibilidad de material técnico en español. Aunque existen excelentes recursos en inglés, muchos estudiantes enfrentan una barrera adicional al tener que aprender simultáneamente un nuevo campo de conocimiento y estudiar en un idioma distinto. Este libro busca reducir esa dificultad ofreciendo una exposición rigurosa, pero accesible, completamente en español.

Las explicaciones, ejemplos y ejercicios incluidos aquí han sido utilizados extensivamente por varias generaciones de estudiantes. Muchas de las secciones fueron modificadas repetidamente a partir de sus preguntas, dificultades y comentarios. En ese sentido, este libro no es únicamente el producto de un autor, sino también el resultado de años de interacción con cientos de estudiantes que, sin saberlo, ayudaron a moldear la manera en que estos temas son presentados.

La irrupción de la inteligencia artificial generativa tampoco disminuye la utilidad de un libro como este. Si algo ha demostrado esta nueva etapa del PLN es que disponer de respuestas inmediatas no sustituye la necesidad de comprender los fundamentos. Los modelos actuales facilitan la programación y la experimentación, pero interpretar su funcionamiento, evaluar sus limitaciones, diseñar sistemas robustos o desarrollar nuevas soluciones sigue requiriendo una comprensión sólida de los principios que sustentan la disciplina.

Por ello, este libro pone un énfasis especial en desarrollar la intuición detrás de los modelos, presentar las formulaciones matemáticas esenciales y mostrar la evolución histórica de las ideas que condujeron a los sistemas actuales. Más que memorizar arquitecturas o algoritmos específicos, el objetivo es comprender por qué surgieron, qué problemas resolvieron y cuáles son sus limitaciones.

Si esta obra logra facilitar el aprendizaje de nuevos estudiantes, servir como guía para docentes que diseñan cursos introductorios o contribuir modestamente a ampliar la disponibilidad de literatura técnica de calidad en español, entonces habrá cumplido plenamente su propósito.

**Rubén Manrique**