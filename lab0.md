# Guía para Configuración de un Clúster EMR en AWS

## Parte 1: Creación del Clúster AWS EMR

### Buscar AWS EMR
1. Accede a la consola web de AWS.
2. Busca y selecciona el servicio **EMR**.

### Crear Clúster
1. Configura el nombre y la versión del clúster.
2. Selecciona los paquetes necesarios como **Hadoop** y **Spark**.
3. Activa los catálogos **Glue** y **Hive** para la gestión de tablas.

### Configurar Máquinas EC2
1. Elige la instancia **m5.xlarge**. 
2. Si hay limitaciones de recursos, considera **m4.xlarge** como alternativa.

### Configuración de Software
1. Crea un bucket en **S3** para almacenar notebooks de **JupyterHub**.
2. Configura la persistencia en S3 para JupyterHub con el siguiente código:

    ```json
    [
        {
            "Classification": "jupyter-s3-conf",
            "Properties": {
                "s3.persistence.enabled": "true",
                "s3.persistence.bucket": "tu-bucket"
            }
        }
    ]
    ```

### Seguridad y Roles IAM
1. Configura los grupos de seguridad necesarios.
2. Asigna los siguientes roles de IAM:
   - **Service role**: `EMR_DefaultRole`
   - **Instance profile**: `EMR_EC2_DefaultRole`
   - **Custom automatic scaling role**: `EMR_AutoScaling_DefaultRole`

### Crear el Clúster
- La creación del clúster puede tardar aproximadamente **20 minutos**.

### Abrir Puertos TCP
1. En el grupo de seguridad de la instancia **Master**, abre los puertos necesarios:
   - **22** (SSH)
   - **14000** (Hue)
   - **9870** (HDFS)

---

## Parte 2: Eliminación y Recreación del Clúster
- Los clústeres EMR suelen ser temporales y deben eliminarse cuando no estén en uso.
- Para reutilizar la configuración:
  1. Clona el clúster y configura nuevamente el usuario **hadoop**.
  2. Modifica el archivo `hue.ini` cambiando el puerto **14000** a **9870**.

---

## Parte 3: Ingreso al Clúster EMR con Hue
1. Accede a la aplicación **Hue** en el puerto **8888** usando la IP o el nombre del nodo **Master**.
2. Configura un usuario:
   - **Username**: `hadoop`
   - **Password**: elige una contraseña.

---

## Parte 4: Acceso a JupyterHub
1. Abre **JupyterHub** en el puerto **9443**.
2. Accede con las siguientes credenciales:
   - **Username**: `jovyan`
   - **Password**: `jupyter`
3. Verifica que las variables de contexto de **Spark** estén activas en un notebook **PySpark**.

---

## Referencias
- [Guía oficial de AWS EMR JupyterHub](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-jupyterhub.html)

