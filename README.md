# 🧠 Sistema de Recomendación de Películas con IA Generativa (OpenAI Embeddings)

Este proyecto implementa un **motor de recomendación basado en contenido** usando IA generativa, específicamente **OpenAI Embeddings**, para analizar descripciones y metadatos de películas y recomendar títulos similares.

El sistema utiliza:

- The Movies Dataset (Kaggle)
- Limpieza y preparación de datos en Python
- Embeddings generados con `text-embedding-3-small` (OpenAI)
- Similitud coseno para encontrar películas similares
- Un muestreo de **10,000 películas** para optimizar costo y rendimiento

El objetivo es construir un **prototipo funcional**, modular y fácil de extender para proyectos de ingeniería de IA.

---

## 🚀 1. Arquitectura del sistema

El pipeline del recomendador sigue estos pasos:

1. **Carga del dataset**  
2. **Limpieza mínima necesaria**  
   - Corrección de tipos  
   - Eliminación de películas sin overview  
   - Normalización del ID  
3. **Parseo de columnas JSON**  
   - `genres`, `keywords`, `cast`, `crew`
4. **Construcción del campo `combined_text`**  
   - Overview  
   - Géneros  
   - Keywords  
   - Actores principales  
   - Director  
5. **Muestreo del dataset a 10,000 películas**  
   Esto reduce costo y tiempo de procesamiento sin afectar la calidad del prototipo.  
6. **Generación de embeddings con OpenAI**  
7. **Cálculo de matriz de similitud**  
8. **Función de recomendación `recommend(title, n)`**  
9. **Pruebas con películas reales**

---

## 📦 2. Archivos del repositorio

| Archivo | Descripción |
|--------|-------------|
| `recommender_system.ipynb` | Notebook principal del proyecto (Google Colab) |
| `DATASET.md` | Documentación técnica del dataset usado |
| `README.md` | Documentación general del proyecto |
| `data/` | (Opcional) Archivos CSV del dataset, si se incluyen |

---

## 🛠️ 3. Cómo ejecutar el proyecto

### 1. Clonar el repositorio
```bash
git clone <URL_DEL_REPO>
cd AIE_ING_ALEXGALINDO
````

### 2. Crear archivo `.env` con tu API Key

**Nunca lo subas a GitHub.**

```
OPENAI_API_KEY=tu_api_key_aqui
```

### 3. Abrir el notebook

Recomendado: Google Colab
Archivo:

```
recommender_system.ipynb
```

### 4. Ejecutar las secciones en orden

El notebook está dividido en:

* 1. Introducción
* 2. Instalación de dependencias
* 3. Cargar dataset
* 4. Limpieza
* 5. Preparación del texto combinado
* 6. Generación de embeddings con OpenAI
* 7. Matriz de similitud
* 8. Función de recomendación
* 9. Pruebas
* 10. Conclusiones

---

## 🎬 4. Ejemplo de uso

```python
recommend("Inception", n=5)
```

Salida esperada (ejemplo real del sistema):

```
['Limitless', 'A Scanner Darkly', 'Paranoia', 'Extracted', 'Hardwired']
```

Otro ejemplo:

```python
recommend("Paranoia", n=5)
```

Resultado:

```
['3 Days to Kill', 'Misconduct', 'The Russia House', 'Security', 'Shadow Run']
```

---

## 🧩 5. Decisiones de diseño

### ✔️ Por qué se hizo un muestreo a 10,000 películas

* El dataset completo tiene 45,000 películas
* Usar embeddings en todas multiplica el costo (tokens) y el tiempo
* 10,000 es un punto ideal entre costo, velocidad y calidad del recomendador
* La diversidad temática se mantiene intacta

### ✔️ Por qué usamos content-based en lugar de collaborative filtering

* Ideal cuando no hay ratings suficientes
* Recomendaciones explicables
* Fácil de extender con otros modelos generativos

---

## 🔮 6. Próximos pasos sugeridos

* Agregar búsqueda semántica por texto libre ("películas de hackers")
* Visualización de clusters con PCA / UMAP
* Filtro por género, año o director
* Integración con FastAPI para servir recomendaciones
* Modelo híbrido (content + collaborative filtering)

---

## 👨‍💻 Autor

Proyecto desarrollado como parte de un entrenamiento avanzado en **Ingeniería de IA**, utilizando metodologías aplicadas y herramientas modernas para construcción de sistemas reales de recomendación.

```

---

# 🎉 Listo para pegar en tu GitHub  
Me confirmas cuando lo pegues y guardes el archivo, y avanzamos con:

📌 Revisión final del repositorio  
📌 Sugerencias para subir el notebook  
📌 Cómo hacer tu presentación del proyecto  

Solo dime:

👉 **“Listo, README actualizado”**
```
