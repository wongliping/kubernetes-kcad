# Pods

### Get Pods

```
kubectl get pods
```

|NAME|READY|STATUS|RESTARTS|AGE|
|---|---|---|---|---|
|webapp|1/2|ErrImagePull|0|12s|

`1/2 READY` means that there are 2 containers in `webapp` pod and 1 out of 2 containers are ready.


### Get Pods (Wide Option)

```
kubectl get pods -o wide
```

|NAME|READY|STATUS|RESTARTS|AGE|IP|NODE|NOMINATED NODE|READINESS GATES|
|---|---|---|---|---|---|---|---|---|
|newpods-ndfbf|1/1|Running|0|2m11s|10.244.1.6|node01|< none>|< none>|
|newpods-eiu3d|1/1|Running|0|2m11s|10.244.1.5|node01|< none>|< none>|
|newpods-kl3sf|1/1|Running|0|2m11s|10.244.1.4|node01|< none>|< none>|
|nginx|1/1|Running|0|2m28s|10.244.1.3|node01|< none>|< none>|


### Create Pod

```
kubectl run <pod name> --image=<image name>
```

From yaml file,

```
kubectl apply -f pod-definition.yaml
```

### Describe Pod

```
kubectl describe pod <name of pod>
```

### Delete Pod

```
kubectl delete pod <name of pod>
```

### Generate Pod Yaml Definition (Dry Run)

```
kubectl run <name of pod> --image=<image name> --dry-run=client -o yaml > pod.yaml
```

From the kubernetes API reference, dry-run argument 

> Must be "none", "server", or "client". If client strategy, only print the object that would be sent, without sending it. If server strategy, submit server-side request without persisting the resource.


### Edit Pod

```
kubectl edit pod <name of pod>
```

#### Note on editing existing pods
In any practical quizzes if you are asked to edit an existing pod, note the following

* If you are given a pod definition file, edit that file and use it to create a new pod
* If you are not given a pod definition file, you may extract the definition to a file using the command below

    ```
    kubectl get pod <pod-name> -o yaml > pod-definition.yaml
    ```

    Then edit the file to make the necessary changes, delete and re-create the pod

* Use the `kubectl edit pod <pod-name>` command to edit pod properties

