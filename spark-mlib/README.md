# Spark MLlib: Proyecto de Machine Learning con PySpark

## Descripción

Este repositorio contiene un conjunto completo de notebooks de Jupyter que demuestran el uso de **Apache Spark MLlib** para tareas de Machine Learning. El proyecto cubre desde el preprocesamiento de datos hasta la implementación de algoritmos de aprendizaje supervisado y no supervisado.

**Autor**: Omar Gaston - oy-gastonc@javeriana.edu.co

## Contenido

### 1. Preprocesamiento de Datos (`ML_Preprocesamiento_Omar.ipynb`)

Este notebook muestra técnicas esenciales de limpieza y transformación de datos usando el dataset del Titanic:

- **Identificación y relleno de valores faltantes**
- **Eliminación de duplicados**
- **Eliminación de columnas que no aportan valor**
- **Operaciones Pivot y Explode**
- **Normalización de datos** (StandardScaler y MinMaxScaler)

**Dataset**: `titanic.csv` (891 pasajeros del Titanic)

### 2. Aprendizaje Supervisado (`ML_Supervisado_Omar.ipynb`)

Implementación y comparación de modelos de clasificación para predecir la calidad del vino:

- **Preparación de features** (VectorAssembler, normalización)
- **División Train/Test**
- **Regresión Logística**
- **Random Forest Classifier**
- **Evaluación y comparación de modelos** (matriz de confusión, métricas de precisión)

**Dataset**: `winequality-red.csv` (1,599 muestras de vino tinto de Portugal)

**Problema**: Clasificación binaria (calidad buena ≥ 6 vs. calidad mala < 6)

### 3. Aprendizaje No Supervisado (`ML_NoSupervisado_Omar.ipynb`)

Análisis de clustering para descubrir grupos naturales en los datos de vinos:

- **Preparación de features** (normalización)
- **K-Means Clustering**
- **Bisecting K-Means Clustering**
- **Evaluación de clusters** (Silhouette Score, visualización)

**Dataset**: `winequality-red.csv` (1,599 muestras de vino tinto)

**Objetivo**: Descubrir patrones y grupos naturales basados en propiedades químicas

## Datasets

### Titanic Dataset (`titanic.csv`)
- **Filas**: 891 pasajeros
- **Columnas**: PassengerId, Survived, Pclass, Name, Sex, Age, SibSp, Parch, Ticket, Fare, Cabin, Embarked
- **Características**: Valores faltantes (~20% en Age, ~77% en Cabin), duplicados, columnas inconsistentes

### Wine Quality Dataset (`winequality-red.csv`)
- **Filas**: 1,599 muestras
- **Columnas**: fixed acidity, volatile acidity, citric acid, residual sugar, chlorides, free sulfur dioxide, total sulfur dioxide, density, pH, sulphates, alcohol, quality
- **Características**: Dataset limpio con propiedades químicas medibles del vino

## 🛠️ Tecnologías y Librerías

### Core
- **Apache Spark** (PySpark)
- **Spark MLlib** (Machine Learning library)

### Python Libraries
- `findspark` - Inicialización de Spark
- `pandas` - Manipulación de datos
- `numpy` - Operaciones numéricas
- `matplotlib` - Visualización
- `seaborn` - Visualización estadística

### Spark MLlib Components
- `VectorAssembler` - Creación de vectores de características
- `StandardScaler` - Estandarización (media=0, std=1)
- `MinMaxScaler` - Normalización (rango [0, 1])
- `LogisticRegression` - Regresión logística
- `RandomForestClassifier` - Clasificador de bosque aleatorio
- `KMeans` - Clustering K-Means
- `BisectingKMeans` - Clustering K-Means jerárquico
- `ClusteringEvaluator` - Evaluación de clusters

## Configuración

### Requisitos Previos
- Python 3.11+
- Apache Spark instalado y configurado
- Jupyter Notebook o JupyterLab

### Instalación

```bash
# Instalar dependencias
pip install findspark pandas numpy matplotlib seaborn

# Asegurarse de que Spark esté correctamente configurado
# Configurar variables de entorno si es necesario:
# export SPARK_HOME=/path/to/spark
# export PYTHONPATH=$SPARK_HOME/python:$PYTHONPATH
```

### Configuración de Spark

Los notebooks utilizan configuraciones optimizadas de Spark:

```python
sparkConf = (
    SparkConf()
        .set("spark.scheduler.mode", "FAIR")
        .set("spark.shuffle.io.maxRetries", "10")
        # ... más configuraciones
)
```

## Estructura de los Notebooks

Cada notebook sigue una estructura similar:

1. **Contexto del Problema** - Descripción del dataset y objetivos
2. **Inicialización de Spark** - Configuración de la sesión
3. **Carga y Exploración de Datos** - Análisis exploratorio inicial
4. **Preparación de Features** - Ingeniería de características
5. **Entrenamiento de Modelos** - Implementación de algoritmos
6. **Evaluación** - Métricas y comparación de modelos
7. **Resumen y Conclusiones** - Insights y resultados finales

## Resultados Clave

### Preprocesamiento
- Identificación y manejo de valores faltantes
- Eliminación de duplicados y columnas innecesarias
- Transformaciones con Pivot y Explode
- Normalización de datos para ML

### Aprendizaje Supervisado
- Comparación entre Regresión Logística y Random Forest
- Evaluación mediante matriz de confusión y métricas de precisión
- Identificación del mejor modelo para clasificación de calidad de vino

### Aprendizaje No Supervisado
- Descubrimiento de grupos naturales en los datos
- Comparación entre K-Means y Bisecting K-Means
- Evaluación mediante Silhouette Score y visualización

## Documentación Adicional

- `Evaluaciones de PySpark.pdf` - Documentación adicional sobre evaluaciones de PySpark

## Autor

**Omar Gaston**
- Email: oy-gastonc@javeriana.edu.co
- Universidad: Pontificia Universidad Javeriana (PUJ)

## Notas

- Los notebooks están diseñados para ejecutarse en entornos con al menos **4 cores** y **4GB de memoria** para un rendimiento óptimo
- Se recomienda revisar la configuración de Spark según los recursos disponibles
- Los datasets están incluidos en el repositorio para facilitar la reproducción de los experimentos

## Referencias

- [Apache Spark Documentation](https://spark.apache.org/docs/latest/)
- [Spark MLlib Guide](https://spark.apache.org/docs/latest/ml-guide.html)
- [PySpark API Reference](https://spark.apache.org/docs/latest/api/python/)

