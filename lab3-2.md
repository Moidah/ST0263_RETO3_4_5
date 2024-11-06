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

