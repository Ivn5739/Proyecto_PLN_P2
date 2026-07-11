# Agente Conversacional para Admisión y Nivelación - Universidad de Guayaquil

Chatbot basado en técnicas clásicas de Procesamiento de Lenguaje Natural (TF-IDF, similitud coseno,
extracción de entidades por reglas/regex y respuesta de fallback) para responder preguntas frecuentes
sobre el proceso de admisión y nivelación de carrera de la UG.

## Objetivo

Diseñar e implementar un agente conversacional en español que identifique la intención del usuario a
partir de datos reales de fuentes oficiales y devuelva respuestas pertinentes sobre admisión y
nivelación, manejando adecuadamente las consultas no reconocidas (fallback) y extrayendo entidades
relevantes como cédula, fechas y carreras.

## Estructura del repositorio

```
├── data/
│   ├── intents.json         # Intenciones, utterances (patterns) y respuestas
│   ├── entities.json        # Base de conocimiento: bloques y carreras (nombre, semestres)
│   └── test_queries.csv     # 28 consultas de prueba etiquetadas (texto, intent_true)
├── src/
│   └── PLN_ProyectoP2.ipynb # Notebook principal: preprocesamiento, TF-IDF, detección de intención,
│                             # extracción de entidades, chat por consola y evaluación
├── app.py                   # Interfaz web del agente (Streamlit)
├── README.md
└── informe.pdf              # Informe técnico (3-4 páginas) con justificación de decisiones de diseño
```

> Nota: para simplificar la ejecución en Colab, `intents.json`, `entities.json` y `test_queries.csv`
> deben copiarse también en el mismo directorio de trabajo del notebook (o en `data/` si se ajustan las rutas).

## Requisitos

```
pip install scikit-learn pandas nltk unidecode streamlit requests
```

## Ejecución

### Opción 1: Notebook / consola (Google Colab o Jupyter)

1. Abrir `src/PLN_ProyectoP2.ipynb` en Google Colab o Jupyter.
2. Subir o dejar en el mismo directorio los archivos `intents.json`, `entities.json` y `test_queries.csv`.
3. Ejecutar todas las celdas. Se iniciará un chat por consola (`input()`); escribe `salir` para terminar.
4. Al finalizar el chat se ejecuta automáticamente la evaluación sobre `test_queries.csv`, mostrando
   **accuracy** y **F1-macro**, y generando `evaluation_results.csv` con el detalle por consulta.

### Opción 2: Interfaz web (Streamlit)

1. Colocar `app.py`, `intents.json` y `entities.json` en la misma carpeta.
2. Ejecutar:
   ```
   streamlit run app.py
   ```
3. Se abrirá una interfaz de chat en el navegador donde se puede escribir la consulta y ver la
   intención detectada junto con el puntaje de similitud.

## Características principales

- **Preprocesamiento**: minúsculas, eliminación de puntuación, normalización de tildes (unidecode),
  tokenización, eliminación de stopwords en español y stemming (Snowball) como aproximación a lematización.
- **Representación TF-IDF**: unigramas y bigramas (`TfidfVectorizer(ngram_range=(1,2))`).
- **Detección de intención**: similitud coseno contra las utterances de entrenamiento, con umbral de
  confianza (`umbral=0.2`) y respuesta de **fallback** si ninguna intención supera dicho umbral.
- **Extracción de entidades por reglas/regex**:
  - **Carreras**: coincidencia por nombre normalizado contra `entities.json`.
  - **Cédula**: regex `\b\d{10}\b`, con cálculo del último dígito para responder la fecha exacta de
    inscripción/postulación según el cronograma oficial.
  - **Fechas**: regex para fechas en texto ("13 de julio de 2026") y en formato numérico ("13/07/2026").
- **Manejo de errores (`try-except`)**: en la carga de datos (JSON corrupto o falla de red) y en el
  ciclo de conversación (consulta vacía, texto no reconocido o errores inesperados de procesamiento).
- **Evaluación**: métricas de **accuracy** y **F1-macro** sobre 28 consultas de prueba, con reporte de
  errores por consulta.

## Resultados

Ver `evaluation_results.csv` (generado al ejecutar el notebook) y la sección de resultados del
`informe.pdf` para el detalle de accuracy, F1-macro y análisis de errores por intención.

## Fuentes de datos

- Proceso de Admisión: https://admision.ug.edu.ec/admision/
- Curso de Nivelación: https://admision.ug.edu.ec/nivelacion/
- Calendario Académico: https://admision.ug.edu.ec/calendario/
- Carreras universitarias: https://admision.ug.edu.ec/

## Autores

- Iván Andrés Moya Astudillo
- Marco Antonio Moya Ramírez
