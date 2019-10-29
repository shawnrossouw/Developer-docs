Status of docker containers.

```bash
Docker ps
```

Shutdown docker instance. 
```bash
Docker-compose down
```

Spin up docker instance.
```bash
Docker-compose up -d
```
daemon mode(runs in background).
```bash 
-d 
``` 

Run docker command inside project folder where the yml file lives. 

Go Into wordpress files on the container

docker ps - to check what containers are running…

Depending on the container ID, you will either go to the root folder of your project, or will go to the database in your container
```bash
docker exec -it container-id bash
```

If you want to go into the database, go to the docker-compose.yml file and get username and password.

After typing docker exec -it mysql-container-id bash,
You can type 
```bash
mysql -uwordpress(username on yml file) -pwordpress(password on yml file)
```
this will take you into the database

Then type 
```bash
use wordpress;
```
this will select the database


Now you can use all of the above by typing the command
```bash
select * from wp_users;
```
or whatever you need. It will spit out all the items
ONLY USE SEMICOLONS WHEN WORKING IN THE DATABASE
```bash
Exit;
```
to exit out of where your are in the database.
