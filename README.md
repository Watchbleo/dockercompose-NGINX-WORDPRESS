## create a Ubuntu 20.04 EC2 t2.micro ssh, http,
## ssh and run: sudo apt update
## run: sudo apt install docker.io docker-compose -y
create Nginx app called web running in port 8080
sudo docker run --name web -itd -p 8080:80 nginx
now let create a docker compose that will literally do the same and more thing in few clicks 
## mkdir dockerProject --> enter --> cd dockerProject --> nano docker-compose.yaml
create the docker symphony ( commands)

ctrl+x, y enter then run: sudo docker-compose up -d
run: docker-compose ps to show the container that we have deployed.
docker-compose down to shut the container down, docker-compose up -d and docker-compose stop to stop it.
## docker-compose2nodes
now let's deploy a second container with the same image, just make the following adjustment:
under services create another block for website2 port 8082:80 that's it
and run: sudo docker-compose up -d
## dockercomposenetwork. 
 now let create a network for these app in docker-compose and specify the subnet CIDR and IPV4 of the app.
 run sudo docker-compose up -d 
it will create the network for the 2 apps run sudo docker network ls 
and sudo docker inspect dockerproject_bleoweb to show subnet CIDR and IPV4 we specified.
## dockercomposewordpress
now let make more complex. We are going to deploy wordpress with docker-compose
Wordpress has a frontend web layer and also has mysql in the backend.
so we have to deploy both in 2 containers and find a way to connect them.

let cd .. and mkdir wordpress to create a new folder then cd into the folder wordpress
then nano docker-compose.yaml let's define our wordpress inside:
## see docker-compose.yaml 
so we are creating 2 containers one is the wordpress frontend app in which we configured
the DB mysql with user, pwd and name same as the second container which is mysql
and very important we will link them with the function depends_on that will
create a dependency between both and specify the mysql should be created first.
also we will create a volume to backup our data in current directory it will
create a directory called mysql and map that to var/lib/mysql, and create network
once it's deploy go back to your EC2 and add SG 8081, 8082, 8083 then copy paste
the public IP in the browser and test the different port in port 8083 you will see
the wordpress app running and it created mysql folder in your local as well.
