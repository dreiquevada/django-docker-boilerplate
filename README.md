# django-docker-boilerplate
A basic boilerplate for a dockerized Django app with a PostgreSQL database

## Includes:
- **Dockerfile**
    - Contains a basic Dockerfile setup that will:
        - Copy project contents to a container folder (/code)
        - Install the basic packages inside `requirements.txt` file
        - Expose port 80

- **docker-compose** file
    - Contains a basic postgres image with specified credentials. It also exposes a `54322` port so it's easier to connect with PG Admin (or other PostgreSQL GUI tool)
    - Contains the django backend container. You can change the container name by specifying the value for the `container_name`. You can also replace `django_backend` with other name

## Requirements
- [Docker](https://docs.docker.com/engine/install/)
- [docker-compose](https://docs.docker.com/compose/install/) 


## Setup the Django Project
- Run `docker-compose up` - this will build the docker services needed
- Rename the `boilerplate` folder with your desired project name
- In your code editor, replace all instances of 'boilerplate' with your desired project name
- Re-run `docker-compose up`

## Create a Django App
- Run `docker-compose run django_backend django-admin.py startapp <app name>`

## Additional Notes
- Don't forget to add your `.env` file to `.gitignore`
- If you want to use specific version of python packages (e.g. use other Django version), update the `requirements.txt` file and rebuild the project
- If you want to set up a local dev environment for the dockerized project in VSCode, please refer to this [link](https://dev.to/alvarocavalcanti/setting-up-a-python-remote-interpreter-using-docker-1i24). Alternatively, you can just:
    - Install the [Remote-Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) extension
    - Open the Command Pallette and select `Attach to running container`
- Activate container bash: `docker exec -it <container_name> bash`

### Resolve locked directories
By default, the apps folder will be owned by a different user thus requiring you to open the folder as a root user to update the contents. To fix this:
```
sudo chown -R $USER:$USER . 
# OR
sudo chmod -R 777 <project_directory>
``` 

### Resolve docker needing root access
```
sudo groupadd docker
sudo usermod -aG docker ${USER}
sudo systemctl restart docker
sudo chmod 666 /var/run/docker.sock
<logout user and re-login>
```

### Connect database to PGAdmin (or other PostgreSQL GUI tool)
- Just connect using the port and credentials specified in the docker-compose file