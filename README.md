# Docker - INSTALL
Instalaçao Correta do Docker

## 0) instalar virtual box
## 1) snap install docker
## 2) snap connect docker:home
## 3) addgroup --system docker
## 4) adduser $USER docker
## 5) newgrp docker
## 6) snap disable docker
## 7) snap enable docker
# REFERENCIA
- [snap] site: https://github.com/docker/docker-snap
- [rede externa] site: https://stackoverflow.com/questions/36922007/how-to-connect-to-a-docker-container-from-outside-the-host-same-network-osx-1

# DOCKER COMANDOS
- run, start, stop, ps, ps -a, images, commit 
- install dentro do container: tce-load -wi htop

# DOCKER - COMPARTILHAMENTO E MONTAGEM DE PASTA
 docker run -itd --name NOME-CONTAINER -v /DOCKER@PASTA/DOCKER@PASTA/:/PASTA-DO-CONTAINER/PASTA-DO-CONTAINER NOME-IMAGE
# DOCKER - RODAR BASH NO CONTAINER
 docker exec --rm -itd NOME-CONTAINER bin/bash
# DOCKER - EXECUTAR CONTAINER NA PORTA ESPECIFICA
docker run --rm -itd --name NOME-CONTAINER -p PORTA-ENTRADA:PORTA-SERVICO IMAGE
Ex. run --rm -itd --name shiny -p 3838:3838 rocker/rshiny

[cria um container shiny na porta 3838 e disponibiliza na mesma porta]

# DOCKER - COPIA ARQUIVOS
docker cp NOME-CONTAINER:/PASTA /PASTA_DESTINO [DENTRO PARA FORA]

docker cp /PASTA_DESTINO NOME-CONTAINER:/PASTA

# DOCKER-MACHINE
## COMANDOS
docker-machine create -d virtualbox NOME-NODE ( CRIA A MAQUINA-NODE)

docker-machine ssh NOME -> acessa a maquina node


# DOCKER - VOLUME

- $ docker-machine ssh phdrisk mkdir foo ( cria o volume dentro do docker)
- $ docker-machine mount dev:/home/docker/foo pastaLocal ( monta a pasta do docker na pasta local )
### importante: a montante deve ser fora da pasta local
