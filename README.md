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

# DOCKER ( SHINY E RSTUDIO) - UTILIZANDO MESMA DIRETORIA FORA
docker run -d -itd -p 3838:3838 -v /srv/shinyapps/:/srv/shiny-server/ -v /srv/shinylog/:/var/log/shiny-server/ --name phdshiny rocker/shiny

docker run -itd -p 8787:8787 -e PASSWORD=phdrisk -v /srv/shinyapps/:/home/rstudio/shinyapps  --name phdrstudio rocker/rstudio

https://www.edivaldobrito.com.br/instalar-java-no-linux-veja-como-fazer-isso-manualmente/

no prompoy: apt update && apt upgrade && apt gedit ou nano
::: obs no rstudio deve-se instalar o sudo apt install default-jre


Passo 7. Se seu sistema é de 64 bits, use o comando abaixo para baixar o Java. Se o link estiver desatualizado, acesse essa página, baixe a última versão e salve-o com o nome jre-linux.tar.gz;

wget https://javadl.oracle.com/webapps/download/AutoDL?BundleId=241526_1f5b5a70bf22433b84d0e960903adac8 -O jre-linux.tar.gz


Passo 9. Depois de baixar, crie a pasta “jvm” em “/usr/lib” com o comando:

sudo mkdir /usr/lib/jvm

Passo 10. Execute o comando abaixo para descomprimir o pacote baixado, para a pasta criada;

sudo tar zxvf jre-linux.tar.gz -C /usr/lib/jvm

Passo 11. Renomeie a pasta criada. Se ao executar o comando abaixo ocorrer um erro com a mensagem iniciando com “mv: é impossível sobrescrever o não-diretório”, pule este passo;

sudo mv /usr/lib/jvm/jre*/ /usr/lib/jvm/jre

Passo 12. Crie um link simbólico para a pasta criada;

sudo ln -s /usr/lib/jvm/jre /usr/lib/jvm/java-oracle

Como configurar o ambiente Java no Linux manualmente

Para configurar o ambiente Java no Linux manualmente, faça o seguinte:

Passo 1. Crie uma cópia do arquivo /etc/profile;

sudo cp -a /etc/profile /etc/profile.original

Passo 2. Agora abra o arquivo com seu editor de texto favorito;

sudo gedit /etc/profile

Passo 3. Digite ou cole (recomendável) o texto abaixo dentro do arquivo, mais exatamente pouco depois das primeiras linhas (os comentários com símbolo # no inicio da linha). A seguir, salve e feche o arquivo;

JAVA_HOME=/usr/lib/jvm/java-oracle/
PATH=$JAVA_HOME/bin:$PATH export PATH JAVA_HOME
CLASSPATH=$JAVA_HOME/lib/tools.jar
CLASSPATH=.:$CLASSPATH
export  JAVA_HOME  PATH  CLASSPATH

reboot


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
- criar uma TAG : docker tag id ou nome phdriskdocker/nome [antes da barra deve ser sempre o usuario da conta]
- docker push phdriskdocker/nome_image

