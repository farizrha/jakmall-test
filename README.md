### Readme

Name: Fariz Rizky Haykal Abdillah

**README.md** file is the first file that will be read by the engineer.

Create **README.md** file at the project root directory and give specific instructions about how to run this project so each engineer know what to do after they clone the project.

## Steps

1. Base Dockerfile
    
    - Steps:
  
        To build required docker images, simply go to the root host where `docker-compose.yaml` file is located and run command `docker-compose build`.
           
    - Image size:
    
        Result measured by `docker image ls` at `SIZE` column

        - `jakmall/recruitment/cloud-engineer/counter/nginx`: `22.6MB`
        - `jakmall/recruitment/cloud-engineer/counter/php-fpm`: `90.2MB`
        - `jakmall/recruitment/cloud-engineer/counter/php-cli`: `88.7MB`

2. Local Docker Compose

    - Steps:
    
      - Before running the whole service, make sure the .env and .env.local exists with the matching environment variables.
      - I have created `infra` script file to run the whole services and other executions, to initialize the infrastructure for the first time run command `./infra init` where the file is located.
      - Notice in my implementation there is a bug where php artisan migration can't connect with mysql database but then when I shutting down the whole service and running the `./infra init` command again it works just fine to do the migration.
      - There are various commands that can be done by using infra script file, just run command `./infra` or `./infra help` to see more commands available.
      - Check in browser `http://localhost:[DOCKER_COMPOSE_NGINX_HOST_PORT]` where in this case the web counter page is mapped into port 80 so then user can see if the counter page will be counted every time it is refreshed.
      - Check in browser `http://localhost:[DOCKER_COMPOSE_MAILHOG_HOST_PORT]` where in this case the web mail hog is mapped into port 8025 so then user can see if count from web page counter is reported every 5 minutes to web mail hog.
      - Run command ./infra mysql and type password `secret` to login as root to mysql database and see if the migrations is completed. Run command `select * from counter.counter_log;` to see information for every user who access the web counter page.
      - To the ownership of the file of worker service, run command `./infra sh worker` to access worker service and run `ls -lah bootstrap/cache` for example to see the ownership of specific folder.
      - The whole service is working fine, to see if it is working we can run command `./infra logs` or `./infra logs <name of container>` to see if container is working fine.

3. Release

   - Steps:
    
      - I have some problems in release stage where I couldn't answer several task.

