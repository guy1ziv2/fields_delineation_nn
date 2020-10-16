# fields_delineation_nn
Planet Hack 2020 field delineation project

# Using the notebook

We will follow the same procedure as demonstrated in [Planet labs repository](https://github.com/planetlabs/notebooks)
Repeating the steps here for convenience.

### System Prerequisites
* [Docker](https://store.docker.com/search?type=edition&offering=community)
* [Planet Account](https://www.planet.com/explorer/?signup=1)
* [Planet API Key](https://www.planet.com/account/)

### Clone or update repo:

If you've never cloned this repo, run the following:

```bash
git clone https://github.com/guy1ziv2/fields_delineation_nn.git
cd fields_delineation_nn
```

If you have previously cloned this repo in the past, make sure to update to pull any changes locally that might have happened since you last interacted with the notebook:

```bash
cd fields_delineation_nn
git pull
```

## Run Notebooks in Docker
Planet Notebooks rely on a complex stack of technologies that are not always easy to install and properly
configure. To ease this complexity we provide a docker container for running the notebook on docker compatible
systems. To install docker on your system please see docker's [documentation](https://docs.docker.com/engine/installation/)
for your operating system.

### Download prebuilt Docker image (recommended)
The Docker image for these notebooks is hosted in the [planetlabs/notebooks](https://hub.docker.com/r/planetlabs/notebooks) repo on DockerHub. To download and prepare the image for use, run:

```bash
cd fields_delineation_nn
docker pull planetlabs/notebooks
docker tag planetlabs/notebooks planet-notebooks

# Run Docker login if not already logged in
docker login
Enter dockerhub's <username/password>
# If you get errors running the above, you might have to add sudo to the beginning:
#sudo docker pull planetlabs/notebooks
#sudo docker tag planetlabs/notebooks planet-notebooks
```

### Run the container
To run the container (after building or downloading it), add your Planet API key below and issue the following command from the git repository root directory:

```bash
docker run -it --rm -p 8888:8888 -v $PWD:/home/jovyan/work -e PL_API_KEY='[YOUR-API-KEY]' planet-notebooks

# If you get a permissions error running the above, you should add sudo to the front:
# sudo docker run -it --rm -p 8888:8888 -v $PWD:/home/jovyan/work -e PL_API_KEY='[YOUR-API-KEY]' planet-notebooks
```

This does several things:

1. Maps the docker container's ```8888``` port to your system's ```8888``` port.  This makes the
container available to your host systems web browser.

1. Maps a host system path ```$PWD``` to the docker container's working directory.
This ensures that the notebooks you create, edit, and save are available on your host system under the
`jupyter-notebooks` sub-directory and are not *destroyed* when you exit the container.
This also allows for running tests in the `tests` sub-directory.

1. Ensures that the directory in the Docker container named `/home/jovyan/work` that has the notebooks
in them is accessible to the Jupyter notebook server.

1. Starts an interactive terminal that is accessible through http://localhost:8888.

1. Sets an environment variable with your unique Planet API key for authenticating against the API.

1. Includes the ```--rm``` option to clean up the notebook after you exit the process.

### Open Jupyter notebooks
Once the Docker container is running, the CLI output will display a URL that you will use to access Jupyter notebooks
with your browser.
```
http://localhost:8888/?token=<UNIQUE-TOKEN>
```

NOTE: This security token will change every time you start your Docker container.

