# Scripts/Comandos para Lab 3-2

## Usuarios
Ingresar como usuario de Hadoop:

- **username**: hadoop
- **password**: ********

## Archivos de Trabajo
Ubicación temporal en HDFS para los archivos `hdi-data.csv` y `export-data.csv`:

- `/user/hadoop/datasets/onu/hdi`

## Gestión (DDL) y Consultas (DQL)

### Crear la Tabla HDI en HDFS usando Beeline

Tabla manejada por Hive en `/user/hive/warehouse`:

```bash
$ beeline
use usernamedb;
CREATE TABLE HDI (
    id INT,
    country STRING,
    hdi FLOAT,
    lifeex INT,
    mysch INT,
    eysch INT,
    gni INT
) 
ROW FORMAT DELIMITED 
FIELDS TERMINATED BY ',' 
STORED AS TEXTFILE;

```

### Cargar datos a la tabla en HDFS

#### Opción 1: Copiar datos directamente hacia HDFS

```bash
$ hdfs dfs -put hdfs:///user/hadoop/datasets/onu/hdi-data.csv hdfs:///user/hive/warehouse/usernamedb.db/hdi
```
#### Opción 2: Cargar datos desde Hive

Primero, otorgar permisos completos al directorio:

```bash
$ hdfs dfs -chmod -R 777 /user/hadoop/datasets/onu/
$ beeline
0: jdbc:hive2://sandbox-hdp.hortonworks.com:2> LOAD DATA INPATH '/user/hadoop/datasets/onu/hdi-data.csv' INTO TABLE HDI;

```

#### Crear una tabla externa en HDFS

```bash
use usernamedb;
CREATE EXTERNAL TABLE HDI (id INT, country STRING, hdi FLOAT, lifeex INT, mysch INT, eysch INT, gni INT)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
STORED AS TEXTFILE
LOCATION '/user/hadoop/datasets/onu/hdi/';

```

#### Crear la Tabla HDI en EMR/S3/Hue/Hive

Tabla externa en S3

```bash
use usernamedb;
CREATE EXTERNAL TABLE HDI (
    id INT,
    country STRING,
    hdi FLOAT,
    lifeex INT,
    mysch INT,
    eysch INT,
    gni INT
) 
ROW FORMAT DELIMITED 
FIELDS TERMINATED BY ',' 
STORED AS TEXTFILE 
LOCATION 's3://moidah-datasets/onu/hdi/';


```

#### Consultas y Cálculos sobre la Tabla HDI

Mostrar Tablas y Describir la Tabla HDI

```bash
use usernamedb;
show tables;
describe hdi;

```

#### Consultar Todos los Datos de HDI

```bash
select * from hdi;

```

#### Consultar Países con GNI Mayor a 2000

```bash
select country, gni from hdi where gni > 2000;

```

#### Ejecutar un JOIN en Hive

Crear la Tabla EXPO en Hive
Obtener los datos base export-data.csv y ubicarlos en 'datasets'.

```bash
use usernamedb;
CREATE EXTERNAL TABLE EXPO (
    country STRING,
    expct FLOAT
) 
ROW FORMAT DELIMITED 
FIELDS TERMINATED BY ',' 
STORED AS TEXTFILE 
LOCATION 's3://moidah-datasets/onu/export/';

```

Realizar el JOIN entre las Tablas HDI y EXPO
```bash
SELECT h.country, gni, expct 
FROM HDI h 
JOIN EXPO e ON (h.country = e.country) 
WHERE gni > 2000;

```

#### WordCount en Hive

Crear la Tabla docs en Hive para WordCount
Alternativa 1: Usar HDFS

```bash
use usernamedb;
CREATE EXTERNAL TABLE docs (
    line STRING
) 
STORED AS TEXTFILE 
LOCATION 'hdfs://localhost/user/hadoop/datasets/gutenberg-small/';

```

Alternativa 2: Usar S3

```bash
CREATE EXTERNAL TABLE docs (
    line STRING
) 
STORED AS TEXTFILE 
LOCATION 's3://moidah-datasets/gutenberg-small/';
```

#### WordCount Ordenado por Palabra

```bash
SELECT word, count(1) AS count 
FROM (SELECT explode(split(line,' ')) AS word FROM docs) w 
GROUP BY word 
ORDER BY word DESC 
LIMIT 10;

```

#### WordCount Ordenado por Frecuencia de Menor a Mayor

```bash
SELECT word, count(1) AS count 
FROM (SELECT explode(split(line,' ')) AS word FROM docs) w 
GROUP BY word 
ORDER BY count DESC 
LIMIT 10;

```

#### Reto: Almacenar los Resultados de WordCount en una Tabla

Para almacenar los resultados de un WordCount en una tabla en Hive:

1. Crear la Tabla para Almacenar Resultados

```bash
CREATE TABLE wordcount_results (
    word STRING,
    count INT
)
STORED AS TEXTFILE;

```

2. Insertar Resultados del WordCount en la Tabla

```bash
INSERT INTO TABLE wordcount_results
SELECT word, count(1) AS count
FROM (SELECT explode(split(line, ' ')) AS word FROM docs) w
GROUP BY word;

```

3. Consultar la Tabla de Resultados de WordCount

```bash
SELECT * FROM wordcount_results
ORDER BY count DESC
LIMIT 10;

```

#### Resumen del Script Completo

```bash
-- Crear la tabla para almacenar los resultados
CREATE TABLE wordcount_results (
    word STRING,
    count INT
)
STORED AS TEXTFILE;

-- Ejecutar el WordCount e insertar los resultados en la tabla
INSERT INTO TABLE wordcount_results
SELECT word, count(1) AS count
FROM (SELECT explode(split(line, ' ')) AS word FROM docs) w
GROUP BY word;

-- Consultar los resultados de WordCount
SELECT * FROM wordcount_results
ORDER BY count DESC
LIMIT 10;

```
