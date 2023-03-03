### Nginx Vim

docker build -t nginx-vim .
docker run -d -p 80:80 nginx-vim

### Hello Entrypoint CMD

docker build -t hello-entrypoint-cmd .
docker run hello-entrypoint-cmd
docker run hello-entrypoint-cmd X

Nota: 
O entryporint é um comando fixo que é sempre executado
O CMD entra como parametro depois do entrypoint e pode ser substituido

### PHP Laravel

docker build -t miyazakiluiz/php-laravel .
docker run --rm -it -p 8000:8000 miyazakiluiz/php-laravel

docker build -t miyazakiluiz/php-laravel:prod . -f Dockerfile.pro
// imagem otimizada

docker images | grep laravel
// comparando tamanho das imagens

### Utilizando Node via docker

docker run --rm -it -v $(pwd)/:/usr/src/app -p 3000:3000 node:15 bash
// para acessar o container, iniciar o projeto e instalar o express

docker build -t miyazakiluiz/hello-express .
// apos finalizar o desenvolvimento, para disponibilizar a imagem

docker build -t miyazakiluiz/hello-express . -f Dockerfile.prod
// builda a imagem para PRD

docker run --rm -d -p 3000:3000 miyazakiluiz/hello-express 

### Publicando imagens

docker login
docker push <username>/<imagename>

Nota:
<username> é mandatório para subir a imagem no DockerHub


### Network
#### Formatos de Network

Bridge - é necessário fazer o mapeamento de portas, as portas internas do container não são visíveis para o host

Host - as portas dos container são expostas diretamente para o host, sem fazer o mapeamento de portas

Overlay - utilizados para escalabilidade, swarm, cluster

Maclan - atribui um macaddress para um container

None - não possui rede para o container, ele vai rodar de forma isolada

#### Comandos de Network

docker network COMMAND
docker network create --driver bridge <network name>

#### Exemplo Bridge Network

docker network create --driver bridge rede-bash
docker network inspect rede-bash
docker run -dit --name bash1 --network rede-bash bash
docker run -dit --name bash2 --network rede-bash bash
docker run -dit --name bash3 bash

Nesse momento o bash1 consegue enxergar o bash2, mas não o bash3
O comando ping bash2, executado no bash1 retorna sucesso, no bash3 falha

docker exec bash1 ping bash2
docker exec bash1 ping bash3

docker network connect rede-bash bash3

Agora o bash1 enxerga o bash3

docker exec bash1 ping bash3

#### Exemplo Host Network

docker run --rm -d --network host nginx
curl http://localhost

Automaticamente a porta 80 do container nginx é atribuida a porta 80 do localhost
Esse tipo de network funciona em linux e em WSL, porém em Mac ou máquinas virtuais não

#### Acessando localhost pelo container

De dentro do container também é possível acessar o localhost da máquina, mesmo de uma aplicação que não use docker.

Isso é possível através do seguinte endereço:
http://host.docker.internal


### Docker Compose

docker-compose up -d
docker-compose ps
docker-compose down
docker-compose up -d --build

### Comandos MySQL

mysql -uroot -p
show databases;
use nodedb;
create table people(id int not null auto_increment, name varchar(255) not null, primary key(id));
select * from people;