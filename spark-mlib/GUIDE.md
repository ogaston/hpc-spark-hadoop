# Guía de Uso: Notebooks Spark MLlib

Esta guía explica cómo ejecutar los notebooks de este proyecto usando Spark directamente o Docker como alternativa.

## Opción 1: Spark Local (Instalación Directa)

### Requisitos Previos

- Python 3.11+
- Apache Spark 3.5.0 instalado
- Jupyter Notebook o JupyterLab

### Pasos de Configuración

#### 1. Instalar Apache Spark

**Linux/Mac:**
```bash
# Usando Homebrew (Mac)
brew install apache-spark

# O descargar manualmente
wget https://archive.apache.org/dist/spark/spark-3.5.0/spark-3.5.0-bin-hadoop3.tgz
tar -xzf spark-3.5.0-bin-hadoop3.tgz
export SPARK_HOME=/path/to/spark-3.5.0-bin-hadoop3
export PATH=$PATH:$SPARK_HOME/bin
```

#### 2. Instalar Dependencias Python

```bash
pip install findspark pandas numpy matplotlib seaborn jupyter
```

#### 3. Configurar Variables de Entorno (si es necesario)

```bash
# Windows
set SPARK_HOME=C:\spark\spark-3.5.0-bin-hadoop3
set PYTHONPATH=%SPARK_HOME%\python;%SPARK_HOME%\python\lib\py4j-0.10.9.7-src.zip

# Linux/Mac
export SPARK_HOME=/path/to/spark-3.5.0-bin-hadoop3
export PYTHONPATH=$SPARK_HOME/python:$SPARK_HOME/python/lib/py4j-0.10.9.7-src.zip
```

#### 4. Iniciar Jupyter

```bash
jupyter notebook
# o
jupyter lab
```

#### 5. Ejecutar los Notebooks

1. Abrir el notebook deseado (`ML_Preprocesamiento_Omar.ipynb`, `ML_Supervisado_Omar.ipynb`, o `ML_NoSupervisado_Omar.ipynb`)
2. Ejecutar las celdas en orden
3. Los notebooks detectarán automáticamente Spark usando `findspark`

---

## Opción 2: Docker (Recomendado para Entornos Aislados)

### Requisitos Previos

- Docker instalado
- Docker Compose (opcional, pero recomendado)

### Método A: Docker Compose (Más Simple)

#### 1. Crear `docker-compose.yml`

```yaml
version: '3.8'

services:
  jupyter-spark:
    image: jupyter/pyspark-notebook:spark-3.5.0
    container_name: spark-mlib-jupyter
    ports:
      - "8888:8888"
    volumes:
      - .:/home/jovyan/work
    environment:
      - JUPYTER_ENABLE_LAB=yes
    command: start-notebook.sh --NotebookApp.token='' --NotebookApp.password=''
```

#### 2. Iniciar el Contenedor

```bash
docker-compose up -d
```

#### 3. Acceder a Jupyter

Abrir en el navegador: `http://localhost:8888`

#### 4. Detener el Contenedor

```bash
docker-compose down
```

### Método B: Docker Run (Directo)

#### 1. Ejecutar Contenedor

```bash
docker run -d \
  --name spark-mlib-jupyter \
  -p 8888:8888 \
  -v "$(pwd):/home/jovyan/work" \
  jupyter/pyspark-notebook:spark-3.5.0 \
  start-notebook.sh --NotebookApp.token='' --NotebookApp.password=''
```

#### 2. Acceder a Jupyter

Abrir en el navegador: `http://localhost:8888`

#### 3. Ver Logs

```bash
docker logs spark-mlib-jupyter
```

#### 4. Detener y Eliminar

```bash
docker stop spark-mlib-jupyter
docker rm spark-mlib-jupyter
```

### Método C: Dockerfile Personalizado (Más Control)

#### 1. Crear `Dockerfile`

```dockerfile
FROM jupyter/pyspark-notebook:spark-3.5.0

# Instalar dependencias adicionales si es necesario
USER root
RUN apt-get update && apt-get install -y \
    && rm -rf /var/lib/apt/lists/*

USER jovyan
RUN pip install --no-cache-dir \
    findspark \
    pandas \
    numpy \
    matplotlib \
    seaborn

WORKDIR /home/jovyan/work
```

#### 2. Construir y Ejecutar

```bash
# Construir imagen
docker build -t spark-mlib-custom .

# Ejecutar contenedor
docker run -d \
  --name spark-mlib-jupyter \
  -p 8888:8888 \
  -v "$(pwd):/home/jovyan/work" \
  spark-mlib-custom \
  start-notebook.sh --NotebookApp.token='' --NotebookApp.password=''
```

---

## Verificación de la Configuración

### Verificar Spark en el Notebook

Ejecutar esta celda en cualquier notebook para verificar:

```python
import findspark
findspark.init()
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("Test") \
    .getOrCreate()

print(f"Spark Version: {spark.version}")
print("✅ Spark configurado correctamente!")
spark.stop()
```

### Verificar Recursos Disponibles

```python
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("Resource Check") \
    .config("spark.executor.cores", "4") \
    .config("spark.executor.memory", "4g") \
    .getOrCreate()

print(f"Cores disponibles: {spark.sparkContext.defaultParallelism}")
print(f"Memoria del driver: {spark.sparkContext.getConf().get('spark.driver.memory')}")
spark.stop()
```

---

## Solución de Problemas

### Problema: "findspark no encuentra Spark"

**Solución:**
```python
import findspark
findspark.init('/path/to/spark')  # Especificar ruta manualmente
```

### Problema: "OutOfMemoryError"

**Solución:** Ajustar memoria en la configuración de Spark:
```python
sparkConf = (
    SparkConf()
        .set("spark.driver.memory", "2g")  # Reducir si es necesario
        .set("spark.executor.memory", "2g")
)
```

### Problema: "Puerto 8888 ya en uso" (Docker)

**Solución:** Usar otro puerto:
```bash
docker run -d -p 8889:8888 ...
```

### Problema: "No se pueden leer los datasets"

**Solución:** Verificar que los archivos CSV estén en el mismo directorio que los notebooks:
```bash
ls -la *.csv
```

---

## Recursos Recomendados

- **Mínimo**: 4 cores, 4GB RAM
- **Recomendado**: 8 cores, 8GB RAM
- **Óptimo**: 16 cores, 16GB RAM

---

## Notas Importantes

1. **Docker**: Los notebooks y datasets deben estar en el directorio montado como volumen
2. **Spark Local**: Asegúrate de que `SPARK_HOME` esté correctamente configurado
3. **Primera Ejecución**: La primera vez puede tardar más debido a la descarga de dependencias
4. **Memoria**: Ajusta la configuración de memoria según los recursos de tu máquina
