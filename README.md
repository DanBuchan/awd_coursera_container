# Basic Container for Coursera Dockerfile

The following builds a basic docker container containing python3, nginx and visual Studio server. Supervisord is used to handle starting nginx and VS Server.
Nginx acts as a proxy/firewall and handles mapping http requests from outside the container to applications running inside the container.

Make sure you're passingly familiar with docker. A small number of useful docker commands have been summarised in the useful_docker_commands.md markdown.

You should be familiar with linux and specifically ubuntu and the apt-get ecosystem as that will make the `Dockerfile` make more sense.

You must also be familar with the coursera docker build process. Anything you
successfully build must also be run through their build tool to check for safety/security. https://github.com/coursera/coursera-labs. Roughly though, get your docker image working locally. Set up the coursera tool. Then use the `run-lab/run.sh` to build a version and if that works you can zip up your docker  directory and upload your docker info to coursera labs.

To upload to coursera you need to provide a zip of the directory (and all its contents) that contains the `Dockerfile`, `zip -r name.zip .`. Note that you should make the zip file inside directory that contains the dockerfile, don't zip the containing directory as the coursera docker build process assumes the `Dockerfile` is in the vary root of the zip.

When you configure your container on the Coursera Labs Manager page make sure to change the http port to 8000, from the default 8888.

To build a new lab fork the project in git hub and make the edits to the dockerfile that your need

## Things of note

## build.sh

Somewhat over engineered way to call the docker build process

### manifest.json

Used by the coursera docker build tool. Note that the name of the project in the build.sh and here is different. Make sure that's always the case to stop any namespace collisions in your docker images list/set when working locally

### reverse-proxy.conf

configures nginx to map http requests in the browser to the applications running inside you container. So Visual Studio is running on port 8443 and is being mapped to any request for http at /

### supervisord.conf

configures which services, daemons and whatnot are started at runtime when a container starts

## Build

```
sh build.sh
```

## Run and access

```
docker run -p 8888:8000 <name_image>
```

```
docker run -p 8888:8000 coursera_test:dev
```

Access the app at root of localhost:8888 for the Visual Studio interface. Add the path as defined in the

# Workflow

1. Fork this repo to your own container repo
2. Edit the dockerfile to your hearts content
3. Edit the manifest appropriately
4. Build it: sh build.sh
5. Run and access it (i.e. docker run -p 8888:8000 coursera_test:dev)
6. Run run-lab/run.sh to ensure it passes the docker requirements
   ../coursera-labs/run-lab/run.sh build ./
7. zip the whole directory containing the dockerfile using 'zip -r'
8. Upload to coursera labs, follow their instuctions
9. Notably: Configure your lab on the right port and add the files you want to persist. Also ensure the port number is switched from 8888 to 8000
