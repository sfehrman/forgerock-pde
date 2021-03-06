## ForgeRock Personal Development Environment

This project is for everyone who needs to run an instance of the ForgeRock Identity Platform with a small footprint and easy setup. Ideal audiences are developers or people who just want to get to know the ForgeRock Identity Platform but don't want to concern themselves with Kubernetes or traditional installs. The project is setup to support configuration and identity data snapshotting.

### Prerequisites

* [ForgeRock BackStage account](https://backstage.forgerock.com)
* [Docker](https://docs.docker.com/install/) and [Docker Compose](https://docs.docker.com/compose/install/)
* [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [Java Developer Kit](https://adoptopenjdk.net/)

### Prepare the environment

Once you have installed the prerequisite software, clone this repository to your local machine and change to the
training directory:

    git clone https://github.com/vscheuber/forgerock-pde.git
    cd forgerock-pde/

Download the AM and IEC resources,

* to `am/build/resources`
  * [Access Management 6.5.2.2](https://backstage.forgerock.com/downloads/get/familyId:am/productId:am/minorVersion:6.5/version:6.5.2.2/releaseType:full/distribution:eval-war) and rename to `am.war`.
  * [Amster 6.5.2.2](https://backstage.forgerock.com/downloads/get/familyId:am/productId:amster/minorVersion:6.5/version:6.5.2.2/releaseType:full/distribution:zip) and rename to `amster.zip`.
* to `idm/build/resources`
  * [Identity Manager 6.5.0.2](https://backstage.forgerock.com/downloads/get/familyId:idm/productId:idm/minorVersion:6.5/version:6.5.0.2/releaseType:full/distribution:eval-zip) and rename to `idm.zip`.

Run the script `init.sh`. This script performs various preparatory actions with the product binaries, e.g. adds additional authentication nodes and other customizations to the am.war file.

Before you build the docker environment you must add the AM and IDM host names to your system's `/etc/hosts` file, for example run:

    echo "127.0.0.1 am.mytestrun.com idm.mytestrun.com" >> /etc/hosts

### Build and Run

We use `docker-compose` to start containers for AM and IDM on the same network.

Build and start the environment in the background:

    docker-compose up --build

There are many ways to interact with the environment after it has started. To see a list of commands run:

    docker-compose --help

### AM Container

The AM container has been set up with the following properties:

* AM URL: `http://am.mytestrun.com:8090`
* AM admin username: `amadmin`
* AM admin password: `F0rgeR0ck2020`

### IDM Container

The IDM container has been set up with the following properties:

* IDM URL: `http://idm.mytestrun.com:8080/admin`
* IDM admin username: `openidm-admin`
* IDM admin password: `F0rgeR0ck2020`

### Accessing the shell inside the containers

In a new terminal run:

    docker exec -it am bash

or 

    docker exec -it idm bash

to get to the bash shell of each container.
