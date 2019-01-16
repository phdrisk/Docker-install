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
site: https://github.com/docker/docker-snap

# DOCKER - COMPARTILHAMENTO E MONTAGEM DE PASTA
## docker run -itd --name NOME-CONTAINER -v /DOCKER@PASTA/DOCKER@PASTA/:/PASTA-DO-CONTAINER/PASTA-DO-CONTAINER NOME-IMAGE
# DOCKER - RODAR BASH NO CONTAINER
## docker exec --rm -itd NOME-CONTAINER bin/bash
# DOCKER - EXECUTAR CONTAINER NA PORTA ESPECIFICA
## run --rm -itd --name NOME-CONTAINER -p PORTA-ENTRADA:PORTA-SERVICO IMAGE
Ex. run --rm -itd --name shiny -p 3838:3838 rocker/rshiny

[cria um container shiny na porta 3838 e disponibiliza na mesma porta]

# DOCKER - COPIA ARQUIVOS
## docker cp NOME-CONTAINER:/PASTA /PASTA_DESTINO [DENTRO PARA FORA]
## docker cp /PASTA_DESTINO NOME-CONTAINER:/PASTA

# DOCKER-MACHINE
## COMANDOS
### docker-machine ssh NOME -> acessa a maquina docker
