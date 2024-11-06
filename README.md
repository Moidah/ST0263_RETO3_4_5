# ST0263_RETO3_4_5

# Universidad EAFIT

### Curso ST0263 Tópicos Especiales en Telemática, 2024-2
**Retos 3, 4 y 5**  
**Profesor:** Moisés David Arrieta Hernández  
**Correo:** [mdarrietah@eafit.edu.co](mailto:mdarrietah@eafit.edu.co)  

**Nombre:** Edwin Nelson Montoya Munera  
**Correo:** [emontoya@eafit.edu.co](mailto:emontoya@eafit.edu.co)  

---

## Descripción General y Objetivos de los Retos y Laboratorios

Este repositorio contiene los retos y laboratorios desarrollados en el curso ST0263, enfocados en el uso de tecnologías de Big Data, como Hadoop y Spark, para gestionar y procesar grandes volúmenes de información de manera eficiente.

### Lab0: Configuración Inicial de la Infraestructura de Big Data
- **Descripción:** Este laboratorio establece un entorno de trabajo en Amazon EMR (Elastic MapReduce), configurando un clúster de Hadoop en la nube. La finalidad es proporcionar una base técnica para los siguientes laboratorios, permitiendo a los estudiantes familiarizarse con la infraestructura y herramientas de procesamiento de Big Data.
- **Objetivo:** Implementar y poner en marcha un clúster de Amazon EMR con los servicios principales de Hadoop, HDFS y Hue, facilitando la interacción con el sistema de archivos distribuido. Este laboratorio prepara el clúster para los retos posteriores, asegurando la instalación de bibliotecas clave y la configuración básica de seguridad.

### Reto 3 (Lab3-1): Administración de Archivos en HDFS y S3
- **Descripción:** Este reto se centra en la manipulación y organización de archivos dentro de Hadoop Distributed File System (HDFS) y Amazon S3. Los estudiantes explorarán cómo cargar, gestionar y estructurar archivos en un sistema de archivos distribuido y en un entorno de almacenamiento en la nube.
- **Objetivo:** Utilizar comandos de HDFS para ejecutar tareas de administración de archivos, como la creación de directorios, carga de archivos locales a HDFS y transferencia de datos entre HDFS y S3. Este reto permite entender la persistencia de datos en sistemas distribuidos y en la nube.

### Reto 4 (Lab3-2): Consultas y Procesamiento de Datos con Hive y SparkSQL
- **Descripción:** En este reto, los estudiantes aprenderán a realizar consultas y análisis de datos utilizando Hive y SparkSQL sobre datos almacenados en HDFS y S3. Este ejercicio se enfoca en el uso de SQL para gestionar grandes conjuntos de datos estructurados en un entorno de Big Data.
- **Objetivo:** Crear y manipular tablas en Hive para ejecutar consultas SQL en datos almacenados tanto en HDFS como en S3. Este reto incluye la creación de tablas internas y externas, la carga de datos y el uso de SparkSQL para realizar análisis de datos, explorando los formatos de almacenamiento y recuperación de datos.

### Reto 5 (Lab3-3): Análisis de Datos a Gran Escala con PySpark
- **Descripción:** Enfocado en el uso de PySpark, este reto implica realizar análisis exploratorio sobre un conjunto de datos de casos de COVID-19 en Colombia. Los estudiantes aplicarán técnicas de análisis de datos en un entorno distribuido, con la opción de almacenar los resultados en S3 y Google Drive.
- **Objetivo:** Emplear PySpark para procesar grandes volúmenes de datos tanto de manera interactiva como a través de scripts en un clúster distribuido. En este reto, los estudiantes cargarán un conjunto de datos, realizarán análisis exploratorio, filtrado y agregación de información, y almacenarán los resultados en AWS S3 y Google Drive, aprovechando las capacidades de Spark para manejar grandes volúmenes de datos.
