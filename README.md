# st0263-2026-1

## Instalación de docker en AMI Ubuntu:24.04

### Instalar docker en ubuntu:24.04

instalar docker sobre ubuntu 24.04: 
https://docs.docker.com/engine/install/ubuntu/

    sudo usermod -a -G docker ubuntu 

### para AWS:

    sudo usermod -a -G docker ubuntu 

### para GCP: cuando crea las VM le asigna su propio username, fijese en el y cambielo así:
    sudo usermod -a -G docker <username>

### clonar el repositorio del curso

    git clone https://github.com/st0263eafit/st0263-261.git
