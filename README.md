# Basic Container for Coursera Dockerfile

The following builds a basic docker container containing python3, nginx and visual Studio server. Supervisord is used to handle starting nginx and VS Server.
Nginx acts as a proxy/firewall and handles mapping http requests from outside the container to applications running inside the container.

Make sure you're passingly familiar with docker. A small number of useful docker commands have been summarised in the useful_docker_commands.md markdown

You must also be familar with the coursera docker build process. Anything you
succesfully build must also be run through their build tool to check for safety/security. https://github.com/coursera/coursera-labs. Roughly though, get your docker image working locally. Set up the coursera tool. Then use the run-lab/run.sh to build a version and if that works you can upload your docker info to coursera labs.


## Things of note

### manifest.json

Used by the coursera docker build tool.

### reverse-proxy.conf

configures nginx to map http requests in the browser to the applications runnning inside you container

### supervisord.conf

configures which services, daemones and whatnot are started at runtime when a container starts

## Build

```
sh build.sh
```

## Run and access
```
docker run -p 8888:8000 <name_image>
```

Access the app at root of localhost:8000 for the Visual Studio interface. Add the path as defined in the 
