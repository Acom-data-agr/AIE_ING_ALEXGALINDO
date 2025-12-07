# 📄 **Documentación del Dataset — The Movies Dataset (Kaggle)**

## 📌 **Descripción General**

The Movies Dataset es un conjunto de datos ampliamente utilizado para análisis, experimentación y construcción de sistemas de recomendación.
Contiene metadatos de **más de 45,000 películas**, incluyendo:

* Títulos
* Sinopsis (overview)
* Géneros
* Elenco y equipo (cast & crew)
* Palabras clave (keywords)
* Fecha de lanzamiento
* Producción
* Presupuesto y ganancias
* Ratings de usuarios (MovieLens)

El dataset combina información de **TMDB** y **MovieLens**, permitiendo construir sistemas de recomendación tanto de **contenido** como **colaborativos**.

# 🗂️ **Archivos del Dataset**

## 1️⃣ **movies_metadata.csv**

Archivo principal con metadatos de 45k+ películas.

### Campos más importantes:

| Campo                  | Descripción                                          |
| ---------------------- | ---------------------------------------------------- |
| `id`                   | ID de la película en TMDB.                           |
| `title`                | Nombre de la película.                               |
| `overview`             | Descripción o sinopsis. Fundamental para embeddings. |
| `genres`               | Lista de géneros en formato JSON.                    |
| `original_language`    | Idioma original.                                     |
| `release_date`         | Fecha de estreno.                                    |
| `budget`               | Presupuesto.                                         |
| `revenue`              | Recaudación.                                         |
| `runtime`              | Duración.                                            |
| `production_companies` | Compañías productoras (JSON).                        |
| `production_countries` | Países de producción.                                |

### Observaciones:

* Algunos campos vienen como JSON en formato string.
* Tiene valores faltantes o inconsistentes en budget, revenue, y dates.


## 2️⃣ **keywords.csv**

Contiene las palabras clave asociadas a cada película.

| Campo      | Descripción                       |
| ---------- | --------------------------------- |
| `id`       | ID de la película (TMDB)          |
| `keywords` | Lista de keywords en formato JSON |

**Uso:** enriquecer el contenido textual de cada película.

## 3️⃣ **credits.csv**

Contiene el reparto (cast) y equipo técnico (crew).

| Campo  | Descripción                                          |
| ------ | ---------------------------------------------------- |
| `id`   | ID de película                                       |
| `cast` | Lista de actores (JSON)                              |
| `crew` | Lista del equipo técnico (director, productor, etc.) |

**Uso en este proyecto:**
Solo usaremos nombres de actores principales o el director para enriquecer el contenido textual.

## 4️⃣ **links.csv**

Contiene IDs cruzados entre:

* MovieLens
* IMDB
* TMDB

**No lo usaremos para este prototipo.**

## 5️⃣ **links_small.csv**

Versión reducida para pruebas rápidas.

**No se utilizará en este proyecto.**

## 6️⃣ **ratings_small.csv**

Contiene ~100k ratings de usuarios sobre 9k películas.

### Campos:

| Campo | Descripción |
| `userId` | ID de usuario |
| `movieId` | ID MovieLens |
| `rating` | Rating (1–5) |
| `timestamp` | Fecha |

**No se usará en este proyecto**, porque no implementaremos filtrado colaborativo.

# 🧪 **Archivos que usaremos para el prototipo de recomendación basada en contenido**

| Archivo                 | ¿Lo usamos? | Razón                                                               |
| ----------------------- | ----------- | ------------------------------------------------------------------- |
| **movies_metadata.csv** | ✔️          | Contiene overview y géneros, base textual para embeddings.          |
| **keywords.csv**        | ✔️          | Enriquecen el contexto semántico del contenido.                     |
| **credits.csv**         | ✔️          | Podemos extraer nombres de actores/directores como texto adicional. |

# 🚫 **Archivos que NO usaremos**

| Archivo             | Motivo                                                            |
| ------------------- | ----------------------------------------------------------------- |
| `ratings_small.csv` | Es para recomendaciones colaborativas (no aplicará en esta fase). |
| `links.csv`         | IDs cruzados innecesarios para nuestro objetivo.                  |
| `links_small.csv`   | Redundante al no trabajar con ratings.                            |

# 🎯 **Justificación del Subconjunto Seleccionado**

Para un sistema de **recomendación basada completamente en contenido**, es necesario construir representaciones vectoriales (embeddings) a partir del texto descriptivo y etiquetas semánticas de cada película.

Los archivos seleccionados permiten construir un texto enriquecido que incluirá:

* Sinopsis (`overview`)
* Géneros (`genres`)
* Palabras clave (`keywords`)
* Actores principales y director(es) (`credits`)

Con esto formaremos un campo combinado, por ejemplo:

"La historia de un detective... Géneros: acción, crimen... Palabras clave: investigation, murder... Actores: Robert De Niro..."
```

Ese texto será convertido a vectores usando **OpenAI embeddings**, permitiendo cálculos de similitud semántica.

---

# 🤖 **Cómo se usará este dataset en el proyecto**

El prototipo seguirá este flujo:

1. Cargar los archivos `movies_metadata.csv`, `keywords.csv`, `credits.csv`.
2. Hacer **limpieza básica** (solo lo necesario).
3. Convertir listas JSON en texto simple.
4. Crear un campo único `combined_text`.
5. Generar embeddings usando **OpenAI (`text-embedding-3-small`)**.
6. Calcular similitudes entre películas mediante **cosine similarity**.
7. Crear una función:

   ```
   recommend("The Matrix")
   ```

   que devuelva películas similares en su contenido.

# ⚠️ **Limitaciones del dataset**

* Contiene valores faltantes en muchos campos.
* Algunos registros tienen formato incorrecto (especialmente fechas y números).
* JSONs vienen como strings, deben parsearse.
* No todos los `id` coinciden entre archivos (requiere merge cuidadoso).
* No es ideal para modelos colaborativos sin usar ratings completos.

# 📚 **Referencias**

Dataset original en Kaggle:
[https://www.kaggle.com/datasets/rounakbanik/the-movies-dataset](https://www.kaggle.com/datasets/rounakbanik/the-movies-dataset)

TMDB API:
[https://www.themoviedb.org/documentation/api](https://www.themoviedb.org/documentation/api)

MovieLens:
[https://grouplens.org/datasets/movielens/](https://grouplens.org/datasets/movielens/)

