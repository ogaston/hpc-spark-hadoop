# HPC Spark & Hadoop

Repositorio para proyectos y configuraciones relacionadas con **Computación de Alto Rendimiento (HPC)** utilizando Apache Spark y Apache Hadoop.

## Descripción

Este repositorio centraliza proyectos, configuraciones, scripts y documentación relacionados con tecnologías de procesamiento distribuido y big data. Está diseñado para servir como un espacio de trabajo colaborativo para experimentos, análisis y configuraciones de infraestructura de alto rendimiento.

## Objetivos

- **Proyectos de Machine Learning** con Spark MLlib
- **Configuraciones de clusters** Hadoop y Spark
- **Scripts de procesamiento** distribuido
- **Documentación y guías** de implementación
- **Experimentos y análisis** de big data

## Tecnologías

### Apache Spark
- **Spark Core**: Motor de procesamiento distribuido
- **Spark SQL**: Procesamiento de datos estructurados
- **Spark MLlib**: Machine Learning distribuido
- **Spark Streaming**: Procesamiento de datos en tiempo real

### Apache Hadoop
- **HDFS**: Sistema de archivos distribuido
- **MapReduce**: Framework de procesamiento distribuido
- **Hadoop Ecosystem**: Herramientas complementarias (Hive, Pig, HBase, etc.)

## Proyectos Incluidos

### Spark MLlib (`spark-mlib/`)

Proyecto completo de Machine Learning utilizando Spark MLlib que incluye:

- **Preprocesamiento de Datos**: Limpieza, transformación y normalización
- **Aprendizaje Supervisado**: Clasificación con Regresión Logística y Random Forest
- **Aprendizaje No Supervisado**: Clustering con K-Means y Bisecting K-Means

**Ver documentación completa**: [`spark-mlib/README.md`](spark-mlib/README.md)

## Casos de Uso

Este repositorio es útil para:

- **Aprendizaje**: Experimentar con tecnologías de big data
- **Investigación**: Análisis de datos a gran escala
- **Desarrollo**: Prototipado de soluciones distribuidas
- **Educación**: Material didáctico para cursos de HPC
- **Producción**: Configuraciones base para despliegues

## Recursos del Sistema

### Mínimos Recomendados
- **CPU**: 4 cores
- **RAM**: 4GB
- **Disco**: 10GB libres

### Óptimos
- **CPU**: 8+ cores
- **RAM**: 8-16GB
- **Disco**: SSD con 20GB+ libres

### Para Clusters
- **Nodos**: 3+ nodos
- **Red**: Gigabit Ethernet o superior
- **Almacenamiento**: HDFS distribuido

## Contribuciones

Este repositorio está abierto a contribuciones. Para agregar nuevos proyectos:

1. Crear un directorio con nombre descriptivo
2. Incluir un `README.md` con documentación
3. Agregar referencias en este README principal
4. Seguir las convenciones de código existentes

## Notas

- Los proyectos están diseñados para ser ejecutados de forma independiente
- Cada proyecto incluye su propia documentación y guías
- Las configuraciones pueden necesitar ajustes según el entorno
- Se recomienda usar Docker para garantizar consistencia entre entornos

## Referencias y Recursos

### Documentación Oficial
- [Apache Spark Documentation](https://spark.apache.org/docs/latest/)
- [Apache Hadoop Documentation](https://hadoop.apache.org/docs/current/)
- [Spark MLlib Guide](https://spark.apache.org/docs/latest/ml-guide.html)
- [PySpark API Reference](https://spark.apache.org/docs/latest/api/python/)

### Recursos Adicionales
- [Jupyter Project](https://jupyter.org/)
- [Docker Documentation](https://docs.docker.com/)

## Licencia

Este repositorio contiene proyectos educativos y de investigación. Consulta los archivos de licencia individuales en cada proyecto.

## Autores

- **Omar Gaston** - oy-gastonc@javeriana.edu.co
- **Pontificia Universidad Javeriana (PUJ)**

