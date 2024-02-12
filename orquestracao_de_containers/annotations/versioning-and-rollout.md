## Versioning and Rollout

- Each execution of "rollout" will create a revision of the published function.
- Each revision will be assigned a unique revision ID.
- The revision ID is a monotonically increasing identifier, meaning that the revision ID will never be reused.

Now we can rollback to a previous version of the function using the revision ID.

#### Commands

```bash	
kubectl rollout status deployment/<name>
kubectl rollout history deployment/<name>
kubectl rollout undo deployment/<name>
```

#### Strategies types

The default strategy is "RollingUpdate". You can change the strategy type using the following command:

```bash
kubectl patch deployment/<name> -p '{"spec": {"strategy": {"type": "Recreate"}}}'
```

### Basiclly, the deployment have two main strategies for updating the application:

- **Recreate**: The existing pods are killed before new ones are created.
- **RollingUpdate**: The new pods are created before the old ones are killed.

### Advanced strategies

#### The deployment have multiple strategies for updating the application:

- **Recreate**: The existing pods are killed before new ones are created.
- **RollingUpdate**: The new pods are created before the old ones are killed.
- **Blue/Green**: The new version of the application is deployed alongside the old version and traffic is switched between the two versions.
- **Canary**: The new version of the application is deployed to a subset of users or servers and then gradually rolled out to the rest of the infrastructure.
- **A/B Testing**: The new version of the application is deployed to a subset of users or servers and then gradually rolled out to the rest of the infrastructure.
- **Shadow**: The new version of the application is deployed alongside the old version and traffic is sent to both versions, but the traffic to the new version is only for observation.
- **Traffic Splitting**: The new version of the application is deployed alongside the old version and traffic is split between the two versions.



### Updating and Rolling Back Deployments

Kubectl

### Applying a new version of the function

- After updating the spec of the deployment, you can apply the new version of the function using the following command:

```bash
kubectl apply -f deployment.yaml
```

### Rolling back to a previous version of the function

- You can rollback to a previous version of the function using the following command:

```bash
kubectl rollout undo deployment/<name>
```

### Checking the status of the rollout

- You can check the status of the rollout using the following command:

```bash
kubectl rollout status deployment/<name>
```

### Checking the history of the rollout

- You can check the history of the rollout using the following command:

```bash
kubectl rollout history deployment/<name>
```

#### TIP

- When you apply a new version of the function, you can prevent a warning from Kubernetes by adding the --save-config flag to the kubectl apply command.

```bash
kubectl apply -f deployment.yaml --save-config
```

### How Kubernetes manages the updates

The Deployment tool create a new ReplicaSet equal to the previous one, and updates each pod one by one, if the strategy is "RollingUpdate". If the strategy is "Recreate", the Deployment tool will kill all the pods and create new ones.


