# docker-compose
In the docker-compose.yml folder:

* Pull service images
`
docker-compose pull
`

* Create and start containers
`
docker-compose up --detach
`

* Stop services
`
docker-compose stop
`

* Start services
`
docker-compose start
`

* Show logs
`
docker-compose logs
`

## Docker-compose Help
```
manager@docker:~$ docker-compose --help
Usage:  docker compose [OPTIONS] COMMAND
Docker Compose

Options:
      --ansi string                Control when to print ANSI control characters ("never"|"always"|"auto") (default "auto")
      --compatibility              Run compose in backward compatibility mode
      --env-file stringArray       Specify an alternate environment file.
  -f, --file stringArray           Compose configuration files
      --parallel int               Control max parallelism, -1 for unlimited (default -1)
      --profile stringArray        Specify a profile to enable
      --project-directory string   Specify an alternate working directory
                                   (default: the path of the, first specified, Compose file)
  -p, --project-name string        Project name

Commands:
  build       Build or rebuild services
  config      Parse, resolve and render compose file in canonical format
  cp          Copy files/folders between a service container and the local filesystem
  create      Creates containers for a service.
  down        Stop and remove containers, networks
  events      Receive real time events from containers.
  exec        Execute a command in a running container.
  images      List images used by the created containers
  kill        Force stop service containers.
  logs        View output from containers
  ls          List running compose projects
  pause       Pause services
  port        Print the public port for a port binding.
  ps          List containers
  pull        Pull service images
  push        Push service images
  restart     Restart service containers
  rm          Removes stopped service containers
  run         Run a one-off command on a service.
  start       Start services
  stop        Stop services
  top         Display the running processes
  unpause     Unpause services
  up          Create and start containers
  version     Show the Docker Compose version information
```

# Docker
## container
* List all the start containers.
```
manager@docker:~$ sudo docker container ls
CONTAINER ID   IMAGE                            COMMAND                  CREATED      STATUS      PORTS                    NAMES
fd158984d315   greenbone/gsa:stable             "/usr/local/bin/entr…"   7 days ago   Up 7 days   0.0.0.0:9392->80/tcp     openvas-gsa-1
9a4c5590ae1f   greenbone/gvmd:stable            "/usr/local/bin/entr…"   7 days ago   Up 7 days                            openvas-gvmd-1
d9c6e28119c7   greenbone/notus-scanner:stable   "/usr/local/bin/entr…"   7 days ago   Up 7 days                            openvas-notus-scanner-1
...
```

* List all the containers including the ones stopped.
```
manager@docker:~$ docker container ls -a
CONTAINER ID   IMAGE                            COMMAND                  CREATED      STATUS                  PORTS                    NAMES
fd158984d315   greenbone/gsa:stable             "/usr/local/bin/entr…"   7 days ago   Up 7 days               0.0.0.0:9392->80/tcp     openvas-gsa-1
48d7e5ad7741   greenbone/gvm-tools              "/usr/local/bin/entr…"   7 days ago   Exited (0) 7 days ago                            openvas-gvm-tools-1
9a4c5590ae1f   greenbone/gvmd:stable            "/usr/local/bin/entr…"   7 days ago   Up 7 days                                        openvas-gvmd-1
...

```

* Open bash session on a container.
`
docker exec -it fd158984d315 bash
`

* Start a container.
`
docker start fd158984d315
`

* Stop a container.
`
docker stop fd158984d315
`

* Remove  a container.
`
docker rm fd158984d315
`
 
 ### Container Help
```
manager@docker:~$ docker container --help
Usage:  docker container COMMAND
Manage containers

Commands:
  attach      Attach local standard input, output, and error streams to a running container
  commit      Create a new image from a container's changes
  cp          Copy files/folders between a container and the local filesystem
  create      Create a new container
  diff        Inspect changes to files or directories on a container's filesystem
  exec        Run a command in a running container
  export      Export a container's filesystem as a tar archive
  inspect     Display detailed information on one or more containers
  kill        Kill one or more running containers
  logs        Fetch the logs of a container
  ls          List containers
  pause       Pause all processes within one or more containers
  port        List port mappings or a specific mapping for the container
  prune       Remove all stopped containers
  rename      Rename a container
  restart     Restart one or more containers
  rm          Remove one or more containers
  run         Run a command in a new container
  start       Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  top         Display the running processes of a container
  unpause     Unpause all processes within one or more containers
  update      Update configuration of one or more containers
  wait        Block until one or more containers stop, then print their exit codes
```
 
## Network
* List networks
```
manager@docker:~$ docker network ls
Password:
NETWORK ID     NAME              DRIVER    SCOPE
870a7c53e28f   bridge            bridge    local
7ceec7923bfe   host              host      local
e8ed1f5516bd   none              null      local
29ed3d5c5fc3   sec_network       macvlan   local
```

* Create a macvlan network.
`
docker network create -d macvlan -o parent=eth0 --subnet=192.168.1.0/24 --gateway=192.168.1.1 --ip-range=192.168.1.198/32 sec_network
`
 
* Connect a running container to a network.
`
docker network connect sec_network fd158984d315
`

### Network Help
 ```
manager@docker:~$ docker network --help
Password:
Usage:  docker network COMMAND
Manage networks
Commands:
  connect     Connect a container to a network
  create      Create a network
  disconnect  Disconnect a container from a network
  inspect     Display detailed information on one or more networks
  ls          List networks
  prune       Remove all unused networks
  rm          Remove one or more networks 
```
 
 
 ## Docker Help
```
manager@docker:~$ docker --help
Usage:  docker [OPTIONS] COMMAND
A self-sufficient runtime for containers

Options:
      --config string      Location of client config files (default "/var/services/homes/david/.docker")
  -c, --context string     Name of the context to use to connect to the daemon (overrides DOCKER_HOST env var and default context set with "docker context use")
  -D, --debug              Enable debug mode
  -H, --host list          Daemon socket(s) to connect to
  -l, --log-level string   Set the logging level ("debug"|"info"|"warn"|"error"|"fatal") (default "info")
      --tls                Use TLS; implied by --tlsverify
      --tlscacert string   Trust certs signed only by this CA (default "/var/services/homes/david/.docker/ca.pem")
      --tlscert string     Path to TLS certificate file (default "/var/services/homes/david/.docker/cert.pem")
      --tlskey string      Path to TLS key file (default "/var/services/homes/david/.docker/key.pem")
      --tlsverify          Use TLS and verify the remote
  -v, --version            Print version information and quit

Management Commands:
  builder     Manage builds
  config      Manage Docker configs
  container   Manage containers
  context     Manage contexts
  image       Manage images
  manifest    Manage Docker image manifests and manifest lists
  network     Manage networks
  node        Manage Swarm nodes
  plugin      Manage plugins
  secret      Manage Docker secrets
  service     Manage services
  stack       Manage Docker stacks
  swarm       Manage Swarm
  system      Manage Docker
  trust       Manage trust on Docker images
  volume      Manage volumes

Commands:
  attach      Attach local standard input, output, and error streams to a running container
  build       Build an image from a Dockerfile
  commit      Create a new image from a container's changes
  cp          Copy files/folders between a container and the local filesystem
  create      Create a new container
  diff        Inspect changes to files or directories on a container's filesystem
  events      Get real time events from the server
  exec        Run a command in a running container
  export      Export a container's filesystem as a tar archive
  history     Show the history of an image
  images      List images
  import      Import the contents from a tarball to create a filesystem image
  info        Display system-wide information
  inspect     Return low-level information on Docker objects
  kill        Kill one or more running containers
  load        Load an image from a tar archive or STDIN
  login       Log in to a Docker registry
  logout      Log out from a Docker registry
  logs        Fetch the logs of a container
  pause       Pause all processes within one or more containers
  port        List port mappings or a specific mapping for the container
  ps          List containers
  pull        Pull an image or a repository from a registry
  push        Push an image or a repository to a registry
  rename      Rename a container
  restart     Restart one or more containers
  rm          Remove one or more containers
  rmi         Remove one or more images
  run         Run a command in a new container
  save        Save one or more images to a tar archive (streamed to STDOUT by default)
  search      Search the Docker Hub for images
  start       Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
  top         Display the running processes of a container
  unpause     Unpause all processes within one or more containers
  update      Update configuration of one or more containers
  version     Show the Docker version information
  wait        Block until one or more containers stop, then print their exit codes
```
