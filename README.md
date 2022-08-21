# docker_spark_engine
A containerized spark engine create with docker

## pull bitnami/spark image

- on your terminal run: `docker pull bitnami/spark`
- checkout the documentation for that image here: https://hub.docker.com/r/bitnami/spark

## check the docker-compose.yml file and modify it according to your needs

- the bitnami/spark documentation provided above was really useful
- check also the pdf in the more_info folder

## run the docker-compose.yml file to get the image and deploy the containers

- run `docker-compose up -d` in your terminal
- after the procedure is completed, run `docker ps` to check the containers, the master and the workers nodes

## access the spark web ui

- access `http://<host_address>:<connection_port>`. In our case the __host_addres__ is localhost and the __connection port__ is 8080, keep in mind that this is completely customizable

## open the spark-shell

- there are two ways of doing so:

1. __Through the host machine:__ `<spark_unzipped_directory_filepath>/bin/./spark-shell.cmd` `spark://<master_node_address>`. The master node addres is a combination of the container_id port selected at the SPARK_MASTER_URL parameter in the docker-compose.yml file. It is also provided as title of the web ui

2. __Through the master node container:__ First you got to run open an interactive terminal inside the container, in order to do so, run in your terminal `docker exec -i -t <container_name or container_id> bash`. Keep in mind that `docker ps` provides the name and the id of the containers. After openning the terminal inside the container run `<spark_unzipped_directory_filepath>/bin/./spark-shell.cmd` `spark://<master_node_address>`, that is the same command used above in the 1st


## checking data persistence

- run  `docker exec -i -t <container_name or container_id> bash` to open an interactive terminal inside the master node container
- inside the container access the folder we created within the `volumes` parameter in our docker-compose.yml file, `cd /test-files/`
- note that if you run `ls` inside the foldlder you will see the same files as those inside the repo folder. That's how we get persistence, any files and folders created within the test file will be generated in the repo folder. Likewise, any files in the repo folder are accessible in the test-files folder while inside the container!
- `ctrl + D` to leave the container's terminal

## stoping containers

- run `docker stop <container_name or container_id>`  for both containers. 