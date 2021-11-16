#### If you use GitBash in Windows

  In the file **./bash_profile** you must add that :

`alias docker='winpty -Xallow-non-tty -Xplain docker'`


##### Для того чтобы можно было развернуть кластер, вы должны создать ``external network``

<code>docker network create --driver bridge  --subnet=172.21.0.0/16 --gateway 172.21.0.1  zk</code>

######  Проверьте, что сеть создана
 
 <code>docker network ls | grep 'zk'</code>
 
 
#### Запуск развертывания контейнеров

 - Проверяем, что все запустилось.

<code>  docker ps | sort -k7 | grep 'zoo*'</code>

##### Пример удаления контейнеров по маске

docker ps -a | grep 'zoo*' | xargs docker stop | xargs docker rm

##### Нужно скопировать в директорию zookeeper конфигурационный файл

`docker exec -it zookeeper1 bash`

 `docker cp ./src/main/resources/docker/kafka_cluster/zookeepercluster/zoo.cfg zookeeper*:/apache-zookeeper-3.7.0-bin/conf/`

##### Для проверки, нужно зайти в консоль каждого контейнера

`docker exec -it zookeeper* bash`

`zkServer.sh status`