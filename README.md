# Docker - INSTALL
Instalaçao Correta do Docker

## 0) instalar virtual box
## 1) snap install docker - sudo snap install docker
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

# DOCKER - COPIA ARQUIVOS DOCKER-MACHINE - DOCKER CONTAINER
1) MOUNT O ARQUIVO
 
 - a) crie a pasta  na maquina: ex. ~/foo
 - b) cria a pasta dentro do docker-machine  ex. /home/docker/teste
 - c) mount a pasta: docker-machine mount phdrisk:/home/docker/teste foo
 - d) copie para dentro da pasta cp -r shiny/Petrobras6/ foo (local)
  

2) COPIE PARA DENTRO DO DOCKER-MACHIME

phdrisk@phdrisk-desktop:~/shiny$ docker-machine scp -r Petrobras6/  phdrisk:/home/docker/transferencias/

3) COPIE PARA DENTRO DO DOCKER-CONTAINER

docker@phdrisk:~/transferencias$ docker cp Petrobras6 rstudio_shiny:/home/rstudio/ShinyApps/Petrobras



# DOCKER-MACHINE
## COMANDOS


docker-machine create -d virtualbox NOME-NODE ( CRIA A MAQUINA-NODE)

docker-machine ssh NOME -> acessa a maquina node


# DOCKER - VOLUME

- a) $ docker-machine ssh phdrisk mkdir foo ( cria o volume dentro do docker)
- b) $ docker-machine mount dev:/home/docker/foo pastaLocal ( monta a pasta do docker na pasta local )
### importante: a montagem deve ser fora da pasta local (b)
### referencia: https://docs.docker.com/machine/reference/mount/

# DOCKER CONTAINER RSTUDIO/SHINY
-link : https://bioconductor.org/packages/release/bioc/vignettes/sevenbridges/inst/doc/rstudio.html

docker run  --privileged -d -p 8787:8787 -p 3838:3838 --name rstudio_shiny_server sevenbridges/sevenbridges-r

importante os vinculos sao criados, entretanto o rstudio nao deixa alterar ou criar pastas no app

deve-se altear o usuario e dono da pasta /home/rstudio/ShinyApps# chown -Rf rstudio:rstudio 01_hello

# INSTALANDO PACOTES PARA O R_SHINY FUNCIONAR
- apt instal libv8-dev
- library(devtools)
- install_github('lhmet/inmetr')
- install.packages("V8")

# DOCKERHUB
- usuario phdriskdocker
- docker login

## criar uma TAG - para exportar para o dockerhub
- docker tag rocker/shiny phdriskdocker/shiny:version1 {rocker/shiny e o nome da imagem ja existente}
- docker push phdriskdocker/shiny:version1 

- docker imagens - lista os tagnames

- docker rmi phdriskdocker/shiny:version1 {remove a imagem tag}
# PORTAINER
```
docker run -d -p 9000:9000 --name portainer --restart always -v /var/run/docker.sock:/var/run/docker.sock -v /home/renatogroffe/Desenvolvimento/Portainer/data:/data portainer/portainer
```

