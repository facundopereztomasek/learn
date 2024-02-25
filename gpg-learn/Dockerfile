# Utilizamos la imagen base de Ubuntu
FROM ubuntu:latest

# Actualizamos el repositorio
RUN apt-get update

# Instalamos Vim
RUN apt-get install -y vim

# Instalamos Gnupg
RUN apt-get install -y gnupg

# Definimos el directorio de trabajo dentro del contenedor
WORKDIR /practicas_gpg

# Definimos el comando por defecto que se ejecutará al iniciar el contenedor
CMD ["bash"]