# unraid-templates

XML Templates for Unraid

## autoheal

The excellent [willfarrell/autoheal](https://hub.docker.com/r/willfarrell/autoheal) container which (in the absence of Docker native support for it) will restart any docker containers which find themselves in an "unhealthy" state.

**a)** Apply the label `autoheal=true` to your container to have it watched.

**b)** Set ENV `AUTOHEAL_CONTAINER_LABEL=all` to watch all running containers.

**c)** Set ENV `AUTOHEAL_CONTAINER_LABEL` to existing label name that has the value true.

Note: You must apply HEALTHCHECK to your docker images first. See [Docker doco](https://docs.docker.com/engine/reference/builder/#healthcheck) for details.

**ENV Defaults**

```env
AUTOHEAL_CONTAINER_LABEL=autoheal
AUTOHEAL_INTERVAL=5 # check every 5 seconds
AUTOHEAL_START_PERIOD=0 # wait 0 seconds before first health check
AUTOHEAL_DEFAULT_STOP_TIMEOUT=10 # Docker waits max 10 seconds (the Docker default) for a container to stop before killing during restarts (container overridable via label, see below)
DOCKER_SOCK=/var/run/docker.sock # Unix socket for curl requests to Docker API
CURL_TIMEOUT=30 # --max-time seconds for curl requests to Docker API
```

**Optional Container Labels**

Override (per container - in seconds) to stop timeout occuring during container restart
`autoheal.stop.timeout=20`
