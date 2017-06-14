## About

This is a Docker image for [CouchPotato](https://couchpota.to/) - the awesome movie PVR for usenet and torrents.

The Docker image currently supports:

* running CouchPotato under its __own user__ (not `root`)
* support for OpenSSL / HTTPS encryption

## Run

### Run via Docker CLI client

To run the CouchPotato container you can execute:

```bash
docker run --name couchpotato -v <datadir path>:/datadir -v <media path>:/media -p 5050:5050 llamallama/couchpotato
```

Open a browser and point it to [http://my-docker-host:5050](http://my-docker-host:5050)

### Run via Docker Compose

You can also run the CouchPotato container by using [Docker Compose](https://www.docker.com/docker-compose).

If you've cloned the [git repository](https://github.com/domibarton/docker-couchpotato) you can build and run the Docker container locally (without the Docker Hub):

```bash
docker-compose up -d
```

If you want to use the Docker Hub image within your existing Docker Compose file you can use the following YAML snippet:

```yaml
couchpotato:
    image: "llamallama/couchpotato"
    container_name: "couchpotato"
    volumes:
        - "<datadir path>:/datadir"
        - "<media path>:/media"
    ports:
        - "5050:5050"
    restart: always
```

## Configuration

### Volumes

Please mount the following volumes inside your CouchPotato container:

* `/datadir`: Holds all the CouchPotato data files (e.g. config, postProcessing)
* `/media`: Directory for movies

### Configuration file

By default the CouchPotato configuration is located on `/datadir/config.ini`.
If you want to change this you've to set the `CONFIG` environment variable, for example:

```
CONFIG=/datadir/couchpotato.ini
```
