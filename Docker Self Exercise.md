
---

## Self Exercises – Tasks 

### Part 1: Getting Started with Docker

**Task 1: Launch Your First Interactive Container**
- Pull the `alpine` image from Docker Hub.
- Run a container in interactive mode named `myalpine`.
- Inside the container, create a file called `hello.txt`.
- Display the list of files.
- Exit the container.
- View the list of all containers, including stopped ones.

**Task 2: Understanding Container Interaction**
- Start a new container from the `debian` image with the name `deb01`.
- Install the `curl` package inside the container.
- Use `curl` to access `https://example.com` and verify the output.
- Exit the container.
- Reattach to the running container.
- Exit again using keyboard shortcut `Ctrl+P+Q`.
- Use `docker exec` to run `ls /` inside the container.

**Task 3: Working with Detached Mode and Web Services**
- Run a container named `myweb` using the `httpd` image in detached mode.
- Verify that the container is running.
- Execute a bash shell inside the container and check the web server root directory (`/usr/local/apache2/htdocs`).
- Stop and remove the container.
- Remove the image used by the container.

---

### Part 2: Docker Lifecycle Practice

**Task 4: Lifecycle Management with a Database Image**
- Pull the `mysql:5.7` image.
- Create a container named `dbtest` but do not start it.
- Start the container with a root password set using environment variables.
- Pause the running container.
- Unpause it.
- View container logs.
- Use `docker stats` to monitor its resource usage.
- Stop the container and remove it.

**Task 5: Clean Up Docker Environment**
- List all images and containers.
- Remove all stopped containers.
- Remove unused Docker images.
- Verify that the Docker environment is clean.

---

