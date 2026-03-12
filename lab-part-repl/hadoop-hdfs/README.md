# Levantar el cluster

la primera vez:
    
    docker compose build --no-cache

regularmente:

    docker compose up -d

para bajar:

    docker compose down

# Ver contenedores:
    docker ps

Debe mostrar:

    namenode
    datanode1
    datanode2
    datanode3

# Formatear HDFS (solo la primera vez)

Entrar al namenode:

    docker exec -it namenode bash

Formatear:
    
    hdfs namenode -format

Reiniciar contenedor:

    docker restart namenode

# entender

    docker exec -it namenode bash
    hdfs dfsadmin -report

# Interfaz Web de HDFS
http://localhost:9870

verán:
    DataNodes activos
    bloques
    replicación
    capacidad

# Entrar al namenode
    docker exec -it namenode bash

# Ver HDFS
    hdfs dfs -ls /

# Comando clave del laboratorio
Este es el más importante para explicar replicación y particionamiento:

    hdfs fsck /archivo -files -blocks -locations

verán algo como:
    Block replica on datanode1
    Block replica on datanode2
    Block replica on datanode3

# gestion de archivos y directorios en HDFS

    hdfs dfs -mkdir /data
    hdfs dfs -ls /

# crear un archivo de 200 MB

    dd if=/dev/urandom of=bigfile.txt bs=1M count=200

# copiarlo a HDFS

    hdfs dfs -put bigfile.txt /data

# analizar particionamiento y replicación

    hdfs fsck /data/bigfile.txt -files -blocks -locations

# visualizar bloques 

    hdfs dfs -stat %b /data/bigfile.txt

# Ver tamaño de bloques:

    hdfs getconf -confKey dfs.blocksize

# Cambiar replicación a 3:
    
    hdfs dfs -setrep -w 3 /data/bigfile.txt

# Verificar:

    hdfs fsck /data/bigfile.txt -blocks -locations

verán:

    Replica on datanode1
    Replica on datanode2
    Replica on datanode3

# Simular falla de nodo

Detener nodo:
    
    docker stop datanode2

Revisar estado:

    hdfs dfsadmin -report

HDFS detecta la falla y replica los bloques.

# Preguntas para estudiantes

## Particionamiento
¿Cuántos bloques se generaron para el archivo?
    
    hdfs fsck
## Replicación
¿Cuántas réplicas tiene cada bloque?

## Ubicación
¿En qué nodos se almacenan?

## Tolerancia a fallos
¿Qué ocurre si se apaga un DataNode?

## Balanceo
¿HDFS intenta distribuir bloques equitativamente?