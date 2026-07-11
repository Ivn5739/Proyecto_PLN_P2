# Proyecto PLN P2 - Agente Conversacional para Admisión y Nivelación UG

## Descripción
Este proyecto desarrolla un agente conversacional en español orientado a responder preguntas frecuentes sobre los procesos de admisión y nivelación de la Universidad de Guayaquil (UG). El enfoque del sistema se basa en técnicas clásicas de Procesamiento de Lenguaje Natural (PLN), especialmente representación TF-IDF y similitud coseno para la detección de intenciones, complementado con respuestas predefinidas y manejo de consultas no reconocidas.[file:2][page:3]

El proyecto fue diseñado de acuerdo con el enunciado del Trabajo Parcial II de la asignatura de Procesamiento de Lenguaje Natural, que exige un agente ejecutable localmente y centrado en recuperación de respuestas, no en generación abierta de texto.[file:2]

## Objetivo
Implementar un chatbot académico que identifique la intención del usuario y entregue respuestas pertinentes sobre admisión y nivelación de la UG, utilizando datos reales de fuentes oficiales y mecanismos básicos de extracción de entidades.[file:2]

## Alcance
El sistema contempla un enfoque de PLN clásico con:

- Definición de intenciones y utterances del dominio UG.[file:2]
- Preprocesamiento del texto en español.[file:2]
- Vectorización con TF-IDF.[file:2]
- Comparación mediante similitud coseno.[file:2]
- Respuesta por intención y estrategia de fallback.[file:2]
- Uso de fuentes oficiales de admisión y nivelación UG.[file:2][page:3]

No forma parte del alcance el uso obligatorio de deep learning, transformers o respuestas generativas abiertas.[file:2]

## Estructura sugerida del repositorio

```text
Proyecto_PLN_P2/
├── data/
│   └── intents.json
├── src/
│   ├── preprocessing.py
│   ├── chatbot.py
│   ├── entities.py
│   └── evaluation.py
├── notebooks/
│   └── PLN_ProyectoP2.ipynb
├── docs/
│   └── informe.md
└── README.md
```

La estructura anterior sigue la organización pedida en el enunciado: separación entre datos, código fuente, documentación e informe.[file:2]

## Requisitos funcionales cubiertos

| Requisito | Descripción |
|---|---|
| RF-01 | Definición de 10-15 intenciones, utterances y respuestas en JSON o CSV.[file:2] |
| RF-02 | Limpieza, normalización, tokenización, stopwords y lematización o stemming.[file:2] |
| RF-03 | Representación de frases con TF-IDF usando unigramas o bigramas.[file:2] |
| RF-04 | Detección de intenciones por similitud coseno.[file:2] |
| RF-05 | Extracción de entidades por reglas o expresiones regulares.[file:2] |
| RF-06 | Umbral de confianza y respuesta fallback.[file:2] |
| RF-07 | Ejecución local por consola o interfaz web simple.[file:2] |
| RF-08 | Evaluación con 20-30 consultas y al menos una métrica.[file:2] |

## Fuentes de información
Las intenciones y respuestas del agente deben fundamentarse en fuentes oficiales de la Universidad de Guayaquil. El documento del proyecto menciona, entre otras, el portal oficial de admisión y la página de nivelación UG, además de redes y material de apoyo institucional.[file:2] En el notebook actual también se observan enlaces y referencias a estas fuentes como base documental del proyecto.[page:3]

## Ejecución general
1. Preparar el archivo de intenciones en formato JSON o CSV.
2. Ejecutar el preprocesamiento del texto.
3. Ajustar el vectorizador TF-IDF con las utterances del sistema.
4. Procesar la consulta del usuario.
5. Calcular la similitud coseno con las frases registradas.
6. Seleccionar la intención con mayor puntaje o activar el fallback si el valor no supera el umbral.[file:2]

## Tecnologías esperadas
- Python 3.
- scikit-learn para TF-IDF y similitud coseno.
- NLTK o spaCy para preprocesamiento en español.[file:2]
- Jupyter Notebook o Google Colab para experimentación local.[page:3]

## Entregables académicos
El enunciado exige entregar un repositorio de GitHub con datos, código fuente, README, archivos para reproducir el análisis y un informe escrito de 3-4 páginas en PDF.[file:2] La entrega en Moodle consiste únicamente en el enlace al repositorio accesible para el docente.[file:2]
