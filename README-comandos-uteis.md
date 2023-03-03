## Comandos Úteis

sudo service docker start
// inicia docker no wsl

docker ps 

docker run hello-world

docker ps -a
// -a lista containers que executaram no passado

docker run -it --rm ubuntu bash
// bash eh o comando que vai ser executado ao subir o container
// -i modo interativo
// -t tty permitir executar comandos no terminal
// --rm remove container do historico apos finalizar

docker start <container name/id>
docker stop <container name/id>
docker rm <container name/id>
// remove container

docker run -d -p 8080:80 --name nginx nginx
// -p 8080:80 , mapeia a porta 8080 do localhost para a porta 80 do container
// -d , detach, libera o terminal do proceso
// --name atribui um nome para o container, no caso do exemplo nginx

docker exec [-it] <container name/id> <command>

docker run -d --mount type=bind,source=“$(pwd)”/<folder>,target=/<path>/<folder>

docker run -d --mount type=volume,source=<volume name>,target=/<path>/<folder>

docker volume COMMAND
docker volume ls
docker volume create <volume name>

docker images
docker pull <image name>
docker rmi <image name>
docker ps -a -q
// lista ids de todos os containers

docker rm $(docker ps -a -q) -f
// remove todos os container

docker attach <image name>
// comando utilizado para acessar o terminal do container depois de ter dado o detach “-d”

docker logs <container name/id>