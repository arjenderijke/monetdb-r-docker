monetdb-r-docker
===========================
Docker container for [MonetDB with R](https://www.monetdb.org/content/embedded-r-monetdb)

Based on Fedora (latest)

![docker-badge](http://dockeri.co/image/monetdb/monetdb-r-docker)

# Launching a MonetDB container
Pull the image from the registry:

```
docker pull monetdb/monetdb-r-docker
```

## Quick start
```
docker run -d -P --name monetdb-r monetdb/monetdb-r-docker
```
The `-d` option will send the docker process to the background. The `-P` option will publish all exposed ports.

After that, you should be able to access MonetDB on the default port `50000`, with the default username/password: `monetdb/monetdb`.

Or you can run `docker exec -it monetdb-r mclient db` to open an [`mclient`](https://www.monetdb.org/Documentation/mclient-man-page) shell in the container.

## Production run
Before letting other users access the database-in-container, you should set a new password for the admin user `monetdb`:

```
docker exec -d monetdb-r /root/set-monetdb-password.sh <password>
```

# Advanced
## Multiple database servers per container
The MonetDB daemon [monetdbd](https://www.monetdb.org/Documentation/monetdbd-man-page) allows for multiple MonetDB database server processes to run on the same system and listed on the same port. While it is not advised to run more than one database server in the same Docker container, you can do that by creating a new database with the [monetdb](https://www.monetdb.org/Documentation/monetdb-man-page) command-line control tool. In this container, the database server is controller by the MonetDB daemon (`monetdbd`), both of which are started by `supervisord`.

For more information on how to use MonetDB, check out the [tutorial](https://www.monetdb.org/Documentation/UserGuide/Tutorial).

## Build your own
You can use the image as a base image when building your own version.
After pulling the image from the registry, run the command bellow to build and tag your own version.

```
docker build --rm -t <yourname>/monetdb-r-docker .
```

# Details
## Base image
The MonetDB image is based on the latest Fedora (at the time of image generation). There are plans to migrate to CentOS (latest) once certain system.d issue is resovled
## Software
The image includes the latest stable version (at the time of image generation, again) of:
* MonetDB
* GEOS module
* R integration module
* R

The default database on the image has R integration enabled.

## Ports
MonetDB runs on port `50000` by default, which is exposed on the image.
