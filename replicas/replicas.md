# Replicas

### Why replicas?

* High availability
* Load balancing and scaling

### Replication Controller V.S. Replica Set

* Both have same purpose but are not the same
* Replication controller is an older technology that is being replaced by replica set. Replica set is the new recommended way to set up replicas

## Replication Controller



## Replica Set

### Create replica set

```bash
kubectl create -f replicaset-definition.yml
```

### Get replica sets

```bash
kubectl get replicaset
```

### Delete replica set

```bash
kubectl delete replicaset <replicaset-name>
```

Note that deleting replicaset also deletes all underlyting pods

### Replace or update replica set

```bash
kubectl replace -f replicaset-definition.yml
```

### Scale

Allows scaling without having to modify the definition file

```bash
kubectl scale --replicas=<desired-no-of-replica> -f replicaset-definition.yml
```

### Generate replica set definition yaml

```bash
kubectl get replicaset <replicaset-name> -o yaml > replicaset-definition.yml
```


## Labels and Selectors

Allows replica sets to identify which pod to monitor and scale when required

```yaml
# replicaset-definition.yml
replica: 3
selector:
    matchLabels:
        tier: front-end
```

```yaml
# pod-definition.yml
metadata:
    name: myapp-pod
    labels:
        tier: front-end
```

Template section in replica set definition is still required as the replica set may need to create a new pod to maintain the desired number of pod in case one of the pods were to fail in the future. 

## Scale

Options
1. Replace the value of replicas field in replica set definition to desired number and replace it. E.g.

    ```bash
    kubectl replace -f replicaset-definition.yml
    ```

2. Use replicas parameter with original replica set definition. E.g. 

    ```bash
    kubectl scale --replicas=6 -f replicaset-definition.yml
    ```

    This will not change the replicas value in the original replica set definition

3. Use replicas parameter with replica name

    ```bash
    kubectl scale --replicas=6 replicaset myapp-replicaset
    ```

