Alternative CLI tools to Docker

ctr
not very use friendly, but it can pull images and run them. It was solely created for debugging containerd

nerdctl
works very similar to Docker CLI. A lot of the commands are the same.

crictl
Command CRI can work across different container runtimes like rkt.
Again, a debugging tool. So not very easy to use to create containers.
More for the Kubelet perspective. 

|           | Docker                                   | ctr                                     | nerdctl                                | crictl                                  |
|-------------------|------------------------------------------|-----------------------------------------|----------------------------------------|-----------------------------------------|
| Purpose           | Comprehensive container platform.        | Low-level container runtime tool.       | Docker-like CLI for containerd.        | CRI-compatible container runtime CLI.   |
| Community         | Docker, Inc.                             | Containerd project.                     | Associated with containerd.            | Kubernetes project.                     |
| Works With        | Docker Engine.                           | Containerd.                             | Containerd.                            | CRI-compatible runtimes (e.g., containerd, CRI-O). |
| List Containers   | `docker ps -a`                           | `ctr containers list`                   | `nerdctl ps -a`                        | `crictl ps -a`                          |
| Pull Image        | `docker pull [image]`                    | `ctr images pull [image]`               | `nerdctl pull [image]`                 | `crictl pull [image]`                   |
| List Images       | `docker images`                          | `ctr images list`                       | `nerdctl images`                       | `crictl images`                         |
| Run Container     | `docker run [options] [image]`           | `ctr run [image] [container]`           | `nerdctl run [options] [image]`        | `crictl runp [pod config]`              |
| Delete Container  | `docker rm [container]`                  | `ctr containers delete [container]`     | `nerdctl rm [container]`               | `crictl rm [container]`                 |
| Delete Image      | `docker rmi [image]`                     | `ctr images remove [image]`            | `nerdctl rmi [image]`                  | `crictl rmi [image]`                    |
| View Logs         | `docker logs [container]`                | `ctr tasks logs [container]`           | `nerdctl logs [container]`             | `crictl logs [container]`               |
| Execute Command   | `docker exec [container] [command]`      | `ctr tasks exec --exec-id [id] [container] [command]` | `nerdctl exec [container] [command]` | `crictl exec [container] [command]`     |
| Inspect Container | `docker inspect [container]`             | `ctr containers info [container]`      | `nerdctl inspect [container]`          | `crictl inspect [container]`            |
