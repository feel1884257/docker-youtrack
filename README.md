# YouTrack on Docker

This repository contains a Docker image of JetBrains [YouTrack](http://www.jetbrains.com/youtrack).

* The **origin** Docker image is available at [maartenba/youtrack](https://registry.hub.docker.com/u/maartenba/youtrack)
* The **origin** GitHub repository is available at [maartenba/docker-youtrack](https://github.com/maartenba/docker-youtrack)

## Usage

First, pull the Docker image using the following command:

	docker pull propersoft/docker-youtrack

Next, create a container.

	docker run -d propersoft/docker-youtrack

YouTrack starts and listens on port 80 in the container. To map it to the host's port 9001, use the following command to create the container instead:

	docker run --name="youtrack" -p 9001:80 -d propersoft/docker-youtrack

Append custom command to run YouTrack in different context:

```
docker run --name="youtrack-demo" -p 9988:80 -d propersoft/docker-youtrack java -Xmx1g -XX:MaxPermSize=250m -Djava.awt.headless=true -jar youtrack.jar 80/demo
```

### Additional settings

YouTrack stores its data and backups at ```/root/teamsysdata``` and ```/root/teamsysdata-backup```
and its logs at `/root/.youtrack/logs` in the container.
If you wish to re-use data, it is a good idea to set up a volume mapping for these paths. For example:

	docker run --name="youtrack" -v /home/ds/youtrack/teamsysdata:/root/teamsysdata -v /home/ds/youtrack/teamsysdata-backup:/root/teamsysdata-backup -v /home/ds/youtrack/.youtrack/logs:/root/.youtrack/logs -p 9001:80 -d propersoft/docker-youtrack:latest
