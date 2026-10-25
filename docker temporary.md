- video watched: https://www.youtube.com/watch?v=fqMOX6JJhGo&t=1305s
# Commands

**to start a container**

```bash
docker run -d -p 8080:80 --name my-app php:8.2-apache
```

- **`docker run`**: Instructs Docker to launch a container.
- **`-d`**: Runs it in the background.
- **`-p 8080:80`**: Maps port `8080` on your machine to port `80` (Apache's web server port) inside the container.
- **`--name my_php_app`**: Names the container `my_php_app`.
- **`php:8.2-apache`**: Specifies the base image to pull and run.
	- the text after the colone is the tag, if we dont specify a tag the default tag will be **`latest`**

If this image is not already saved on your local machine, Docker automatically downloads it from **Docker Hub** (the public registry for container images).

**to see all containers**

```bash
docker ps -a
```

- **`-a`**: includes containers that are not active (stopped or crashed)

**stopping containers**

```bash
docker stop container1_id container2_name
```

- to stop a container we need either their name or their id in which we can get from the ps command

**delete a container**

to save up space from the disk we can delete containers 

```bash
docker rm -f my_php_app;
```

- **`-f`** paramter will stop the container then delete it, by default active containers cant be deleted
- also the same thing with id and name applies here

**searching for images**

each container has at max 1 image, to show all images we use the images command but to search for a specific image we add a search text at the end of the command

```bash
docker images php
```

**deleting an image**

after finding the image we want to delete we first have to remove all containers that have image installed on it

```bash
docker rmi image-name
```

- just like others ID also works

**downloading images without running them in containers**

`docker pull` explicitly downloads an image blueprint from a remote container registry (by default, Docker Hub) to your local hard drive **without creating or running a container**.

```bash
docker pull imageName
```

**Run a Single Command Without opening an interactive terminal**

for example if we want to check the version of php of the image we have on a container we can execute a single command on a container

```bash
# Check PHP version running inside the container
docker exec my_php_app php -v

# Execute a CodeIgniter Spark CLI command directly
docker exec my_php_app php spark migrate
```

**Interactive Terminal (Jump Inside the Container)**

instead if we want to run a series of commands inside a container we can do that using the **`-it`** parameter

```bash
docker exec -it my_php_app bash
```

- if the container doesnt support the bash terminal we can use the sh terminal instead
- to exit the terminal just type **`exit`** and enter

**attach to a container**

normally when we have an application running in a container, we see its output and we cant close the terminal otherwise the container will close as well, that is why make run it is background mode with `-d` but if we want to see the live output  without risking closing our container we can use the attack command

```bash
docker attach my_container
```

- same thing with the id and name feature

**container log**

if we want to instead see all the outputs of our container we run the command

```bash
docker logs container_name
```

**container metadata**

to view informations(metadata) of a container/images we can use the inspect command

```bash
docker inspect object_name
```

# Dockerfile

instead of using built in image from the docker hub, can construct our own docker image by creating the docker file which contains instructions and commands

**Structure**

this file consists of 2 things:

- instructions which are capitalized like RUN
- paramters

**Example**

```bash
# 1. Base image
FROM php:8.2-apache

# 2. Set internal working directory
WORKDIR /var/www/html

# 3. Install system dependencies & PHP extensions needed for web frameworks
RUN apt-get update && apt-get install -y \
    libicu-dev \
    git \
    unzip \
    && docker-php-ext-install intl pdo_mysql

# 4. Copy project code from local machine into container
COPY . /var/www/html

# 5. Document application port
EXPOSE 80

# 6. Default command to keep Apache running in the foreground
CMD ["apache2-foreground"]
```

**Commands**

| **Keyword**   | **Purpose**                                                                                                    | **Timing** |
| ------------- | -------------------------------------------------------------------------------------------------------------- | ---------- |
| **`FROM`**    | Sets the base image foundation (e.g., `php:8.2-apache`, `node:20-alpine`). Must be the first non-comment line. | Build time |
| **`WORKDIR`** | Sets the working directory inside the container for all subsequent `RUN`, `COPY`, and `CMD` commands.          | Build time |
| **`COPY`**    | Transfers files/folders from your host computer into the container filesystem.                                 | Build time |
| **`RUN`**     | Executes terminal commands inside the container during build (e.g., `apt-get install`, `composer install`).    | Build time |
| **`EXPOSE`**  | Documents which port the application listens on (informational metadata).                                      | Runtime    |

**difference between CMD and ENTRYPOINT**

they both are similar and can be used together to extend the functionallty of the docker run command in the terminal

In your Dockerfile, combine them like this:


```bash
# FIXED: The container WILL execute "php spark"
ENTRYPOINT ["php", "spark"]

# DEFAULT ARGUMENT: If the user provides nothing else, use "serve"
CMD ["serve"]
```

**What Happens at Runtime?**

**1. Standard Run (Default behavior)**


```bash
docker run my-ci4-app
```

- **Result:** Executes `php spark serve` (boots the development web server).

**2. Passing a New Argument (`migrate`)**


```bash
docker run my-ci4-app migrate
```

- **Result:** Executes `php spark migrate` (runs database migrations).
- **Why?** Docker kept `ENTRYPOINT` (`php spark`) and replaced `CMD` (`serve`) with `migrate`.

**building command** 

once we are done with creating our own image, we have to build it before running it as a  container

Once your `Dockerfile` is saved in your project root directory, you compile it into an image using:


```bash
docker build -t my-web-app:v1.0 .
```

- **`-t my-web-app:v1.0`**: Tags the image with a custom repository name (`my-web-app`) and version tag (`v1.0`).
- **`.` (Build Context)**: Tells Docker to look in the current working directory for the `Dockerfile` and local files referenced by `COPY`.


# Docker compose

if we want to create multiple containers and images to make a project, we can do that using a compose file that contains all the container that we need to create our project

```yml
services:
  # WEB SERVICE (PHP Web App)
  web:
    build:                      # 1. BUILD SETTINGS
      context: .
      dockerfile: Dockerfile
    ports:
      - "8080:80"               # Network: Host 8080 -> Container 80
    volumes:
      - .:/var/www/html         # 2. STORAGE: Bind mount (Live code updates)
    environment:
      - DB_HOST=db              # 3. NETWORKING: Points directly to 'db' service name

  # DATABASE SERVICE (MySQL)
  db:
    image: mysql:8.0
    environment:
      MYSQL_DATABASE: my_app
      MYSQL_ROOT_PASSWORD: secret
    env_file: 
    - .env # Reads secrets directly from your untracked local .env file
    volumes:
      - db_data:/var/lib/mysql  # 2. STORAGE: Named volume (Persistent storage)

# GLOBAL STORAGE DEFINITIONS
volumes:
  db_data:                      # Declares named volume so MySQL data survives container restarts
```

**parameters**

| **Parameter**        | **Purpose**                                                                                                                                                                                                                                        | **Example**                    |
| -------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------ |
| **`services:`**      | Top-level block defining all application containers to manage.                                                                                                                                                                                     | `services:`                    |
| **`<service_name>`** | Custom identifier for a specific container (also acts as its network hostname).                                                                                                                                                                    | `web:` or `db:`                |
| **`image:`**         | Specifies a pre-built image to pull directly from a registry instead of building one.                                                                                                                                                              | `image: mysql:8.0`             |
| **`build:`**         | Instructs Compose to build a custom image using a local `Dockerfile`.                                                                                                                                                                              | `build: .`                     |
| **`context:`**       | Path to the directory containing your project source code and build files.                                                                                                                                                                         | `context: ./backend`           |
| **`dockerfile:`**    | Specifies a custom Dockerfile name if it differs from the default `Dockerfile`.                                                                                                                                                                    | `dockerfile: Dockerfile.dev`   |
| **`ports:`**         | Maps host network ports to container internal ports (`"HOST:CONTAINER"`).                                                                                                                                                                          | `ports: ["8080:80"]`           |
| **`volumes:`**       | Links host paths or managed storage to container folders for real-time sync and data persistence.                                                                                                                                                  | `volumes: [".:/var/www/html"]` |
| **`environment:`**   | Injects key-value environment variables into the running container process.                                                                                                                                                                        | `environment: ["DB_HOST=db"]`  |
| `volumes:`           | top level block that defines the name of the volumes that docker will handle itself(instead of saving it in a known folder docker saves it inside its eternal system files so it doesnt get delete and can be used later) most useful for database | `volumes: db:`                 |
| `env_file:`          | instead of writing secret information like the database password which can be seen by others we can instead link a secrete env file in our directory                                                                                               | `env_file: .env`               |

## Network

for better security its better to divide the front end network from the backend network, here is here to do it

we add a new parameter called network which conatains the name of the network after that we create a global parameter called network that has the name of  our networks with no parameters just like the volumes parameter

```yml
services:
  # 1. FRONTEND: Angular SPA
  frontend:
    build:
      context: ./frontend
      dockerfile: Dockerfile
    ports:
      - "4200:80"                   # Access Angular at http://localhost:4200
    volumes:
      - ./frontend/src:/app/src     # Live code sync for local UI edits
    networks:
      - frontend_net

  # 2. BACKEND: CodeIgniter 4 REST API
  backend:
    build:
      context: ./backend
      dockerfile: Dockerfile
    ports:
      - "8080:80"                   # Access CI4 API at http://localhost:8080
    volumes:
      - ./backend:/var/www/html     # Live code sync for PHP edits
    env_file:
      - .env                        # Passes DB host, credentials, and app keys
    networks:
      - frontend_net
      - backend_net

  # 3. DATABASE: MySQL
  db:
    image: mysql:8.0
    restart: always
    env_file:
      - .env
    volumes:
      - db_data:/var/lib/mysql       # Persists database state
    networks:
      - backend_net                 # Isolated from direct public web access

volumes:
  db_data:                          # Standalone Docker volume allocation

networks:
  frontend_net:                     # Shared between Angular and CI4 API
  backend_net:                      # Shared strictly between CI4 API and MySQL
```

## CLI commands

|**Command**|**Purpose**|**Common Flags & Examples**|
|---|---|---|
|**`docker compose up`**|Builds, creates, and starts all services in the background or foreground.|`docker compose up -d` _(Detached mode in background)_<br><br>  <br><br>`docker compose up --build` _(Forces image rebuilds)_|
|**`docker compose down`**|Stops and completely removes containers, networks, and default volumes.|`docker compose down` _(Preserves named volumes)_<br><br>  <br><br>`docker compose down -v` _(Deletes attached named volumes)_|
|**`docker compose ps`**|Lists the current state, runtime status, and port mappings of stack containers.|`docker compose ps`|
|**`docker compose logs`**|Streams terminal logs outputted by services for debugging runtime errors.|`docker compose logs -f` _(Follow live output stream)_<br><br>  <br><br>`docker compose logs -f web` _(Stream specific service)_|
|**`docker compose exec`**|Executes an interactive command or shell session inside a _running_ container.|`docker compose exec web bash`<br><br>  <br><br>`docker compose exec db mysql -u root -p`|
|**`docker compose stop` / `start`**|Pauses or resumes container processes without destroying or removing their state.|`docker compose stop`<br><br>  <br><br>`docker compose start`|
|**`docker compose restart`**|Restarts all or specified running services without recreating containers.|`docker compose restart backend`|


