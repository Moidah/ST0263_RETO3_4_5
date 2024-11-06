# Scripts/Comandos para Lab 3-1

### Conexión por SSH a la Instancia
```bash
ssh -i <your-key-pair.pem> hadoop@<master-public-dns-name>

```
## Verificar Directorios en HDFS

Para listar los directorios en el sistema de archivos HDFS:

```bash
hdfs dfs -ls /
hdfs dfs -ls /user
hdfs dfs -ls /user/hadoop
hdfs dfs -ls /user/hadoop/datasets

```

### Instalación de Git

```bash
sudo yum install git
```

### Clonación del repositorio

```bash
git clone https://github.com/st0263eafit/st0263-242.git

```

### Crear directorios en HDFS

Crear los directorios necesarios en HDFS

```bash
hdfs dfs -mkdir /user/hadoop/datasets
hdfs dfs -mkdir /user/hadoop/datasets/gutenberg

```

### Cargar archivos a HDFS

Cargar los archivos desde el sistema local a HDFS:

```bash
hdfs dfs -put /home/ec2-home/st0263-242/bigdata/datasets/gutenberg-small/*.txt /user/hadoop/datasets/gutenberg/
hdfs dfs -copyFromLocal /home/ec2-home/st0263-242/bigdata/datasets/gutenberg-small/*.txt /user/hadoop/datasets/gutenberg/

```

### Verificar archivos cargados

```bash
hdfs dfs -ls /user/hadoop/datasets
hdfs dfs -ls /user/hadoop/datasets/gutenberg-small

```

### Obtener archivos de HDFS a la máquina local

Descargar los archivos desde HDFS a la maquina local

```bash
hdfs dfs -get /user/hadoop/datasets/gutenberg-small/*.txt ~hadoop/mis_datasets/
hdfs dfs -copyToLocal /user/hadoop/datasets/gutenberg-small/*.txt ~hadoop/mis_datasets/

```

### Listar archivos en la carpeta local

Listar los archivos en la carpeta local mis_datasets:

```bash
ls -l mis_datasets

```

### Creación de carpetas en HDFS y copiar de archivos

```bash
hdfs dfs -mkdir /user/hadoop/datasets
hdfs dfs -mkdir /user/hadoop/datasets/gutenberg-small
hdfs dfs -put /local-path-to-cloned-repo/* /user/hadoop/datasets/gutenberg-small

```

### Copiar archivos a Hive

Cargar los archivos en HDFS para ser utilizados por Hive:

```bash
hdfs dfs -put /root/st0263-242/bigdata/datasets/gutenberg-small/*.txt /user/hadoop/datasets/gutenberg-small/

```

### Copiar archivos a S3

Subir losarchivos a un bucket de Amazon S3

```bash
hadoop fs -put /root/st0263-242/bigdata/datasets/ s3://moidah-datasets/

```

### Copiar archivos hacia el AWS S3 vía SSH

Envia los archivos a S3 usando comando de Hadoop a traves de SSH:

```bash
hadoop fs -put /root/st0263-242/bigdata/datasets/ s3://moidah-datasets/

```

