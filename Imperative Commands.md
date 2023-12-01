In Kubernetes, while you'll primarily use declarative methods with YAML files, imperative commands are useful for quick, one-time tasks and for creating YAML template files efficiently, saving time during the CKAD exam.

Key options to know for `kubectl`:

- `--dry-run=client`: Tests the command ***without creating*** the resource, confirming if it's correctly formatted.
  
- `-o yaml`: Outputs the resource definition in YAML format.
  
- `> nginx-pod.yaml` placed at the end of command: Pipes the output to definition file: `nginx-pod.yaml`

Combine these options to swiftly generate YAML templates, which you can then edit and use to create resources, bypassing the need to write them from scratch.

### Pods

| Command | Description | Example |
|---------|-------------|---------|
| `kubectl run` | Create a pod | `kubectl run mypod --image=nginx --restart=Never` |
| `kubectl run` with `--dry-run=client -o yaml` | Generate a pod YAML template | `kubectl run mypod --image=nginx --restart=Never --dry-run=client -o yaml > mypod.yaml` |
| `kubectl delete pod` | Delete a pod | `kubectl delete pod mypod` |
| `kubectl get pods` | List all pods | `kubectl get pods` |
| `kubectl describe pod` | Get detailed info about a pod | `kubectl describe pod mypod` |
| `kubectl attach` | Attach to a running pod interactively | `kubectl attach mypod -i` |
| `kubectl exec` | Execute a command in a pod | `kubectl exec mypod -- ls /usr/share/nginx/html` |
| `kubectl port-forward` | Forward local port to a pod | `kubectl port-forward mypod 8080:80` |
| `kubectl cp` | Copy files to/from a pod | To Pod: `kubectl cp ./localfile.txt mypod:/path/in/pod/localfile.txt` <br> From Pod: `kubectl cp mypod:/path/in/pod/localfile.txt ./localfile.txt` |
| `kubectl run` with resource limits | Create a pod with specific resource limits | `kubectl run mypod --image=nginx --restart=Never --requests='cpu=100m,memory=256Mi' --limits='cpu=200m,memory=512Mi'` |

### Deployments

| Command | Description | Example |
|---------|-------------|---------|
| `kubectl create deployment` | Create a deployment | `kubectl create deployment mydeployment --image=nginx` |
| `kubectl create deployment` with `--dry-run=client -o yaml` | Generate a deployment YAML template | `kubectl create deployment mydeployment --image=nginx --dry-run=client -o yaml > mydeployment.yaml` |
| `kubectl create deployment` with replicas | Create a deployment with specific replicas | `kubectl create deployment mydeployment --image=nginx --replicas=4` |
| `kubectl delete deployment` | Delete a deployment | `kubectl delete deployment mydeployment` |
| `kubectl scale deployment` | Scale a deployment | `kubectl scale deployment mydeployment --replicas=3` |
| `kubectl set image deployment` | Update the image of a deployment | `kubectl set image deployment/mydeployment nginx=nginx:1.9.1` |
| `kubectl rollout undo deployment` | Roll back a deployment | `kubectl rollout undo deployment mydeployment` |
| `kubectl rollout history deployment` | View rollout history of a deployment | `kubectl rollout history deployment mydeployment` |
| `kubectl rollout pause deployment` / `kubectl rollout resume deployment` | Pause and resume a deployment | Pause: `kubectl rollout pause deployment mydeployment` <br> Resume: `kubectl rollout resume deployment mydeployment` |
| `kubectl get deployments` | Get deployment information | `kubectl get deployments` |
| `kubectl describe deployment` | Describe a deployment | `kubectl describe deployment mydeployment` |


### Services
| Command | Description | Example |
|---------|-------------|---------|
| `kubectl expose deployment` | Expose a deployment as a service | `kubectl expose deployment mydeployment --type=LoadBalancer --port=80` |
| `kubectl expose` **\*** | Expose an existing pod as a service | `kubectl expose pod mypod --port=80 --target-port=8080` |
| `kubectl create service` | Create a service from scratch | `kubectl create service clusterip myservice --tcp=5678:8080` |
| `kubectl create service nodeport` **\*\*** | Create a NodePort service with a specific node port | `kubectl create service nodeport nginx --tcp=80:80 --node-port=30080 --dry-run=client -o yaml` |
| `kubectl delete service` | Delete a service | `kubectl delete service myservice` |
| `kubectl get services` | List all services | `kubectl get services` |
| `kubectl describe service` | Describe a service | `kubectl describe service myservice` |
| `kubectl create service` with `--dry-run=client -o yaml` | Generate a service YAML template | `kubectl create service clusterip myservice --tcp=5678:8080 --dry-run=client -o yaml > myservice.yaml` |
| `kubectl edit service` | Edit a service | `kubectl edit service myservice` |
##### Note the Trade-offs
**\*** **Exposing an existing pod as a service:**
This command is used to create a service that exposes an existing pod. Remember that you ***cannot specify the node port directly*** with this command. For node port configuration, either use the imperative command to generate the service with `--nodePort` or generate the service definition file first then manually add the node port before creating the service.

\*\* **Creating a NodePort service with a specified node port:**
This command creates a NodePort service and sets a specific node port. Note that this method ***does not use a pod's labels as selectors***, those need to be manually added.
