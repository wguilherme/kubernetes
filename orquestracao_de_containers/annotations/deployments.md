## Deployments

### Annotations
- A deployment generate a ReplicaSet, which in turn generates the Pods. So, when you create a deployment, you are creating:
  - A ReplicaSet
  - N Pods (N is the number of replicas you set in the deployment)

### Resume

- A Deployment is a higher-level API object that manages ReplicaSets and provides declarative updates to Pods along with a lot of other useful features.
- A Deployment provides declarative updates for Pods and ReplicaSets.


#### Rolling release and rolling updates

- Rolling updates allow Deployments' update to take place with zero downtime by incrementally updating Pods instances with new ones.

#### Deployment strategies

- Recreate: The old Pods are killed before the new ones are created.
- RollingUpdate: The new Pods are created before the old ones are killed.
- Blue/Green: The new Pods are created and the old ones are killed at the same time.
- Canary: The new Pods are created and the old ones are killed at the same time, but only a small percentage of the new Pods are created at first.
- A/B Testing: The new Pods are created and the old ones are killed at the same time, but only a small percentage of the new Pods are created at first, and then the percentage is increased over time.
- Shadow: The new Pods are created and the old ones are killed at the same time, but the old ones are not killed until the new ones are ready.
- Traffic Splitting: The new Pods are created and the old ones are killed at the same time, but the traffic is split between the old and new Pods.
  

#### Deployment commands

- `kubectl create deployment <deployment-name> --image=<image-name>` - Create a new deployment.
- `kubectl get deployments` - List all deployments in the cluster.
- `kubectl get deployment <deployment-name>` - List a specific deployment in the cluster.
- `kubectl describe deployment <deployment-name>` - Describe a specific deployment in the cluster.
- `kubectl delete deployment <deployment-name>` - Delete a specific deployment in the cluster.
- `kubectl rollout status deployment <deployment-name>` - Check the status of a specific deployment in the cluster.
- `kubectl rollout history deployment <deployment-name>` - Check the history of a specific deployment in the cluster.
- `kubectl rollout undo deployment <deployment-name>` - Undo a specific deployment in the cluster.
- `kubectl rollout undo deployment <deployment-name> --to-revision=<revision-number>` - Undo a specific deployment to a specific revision in the cluster.
- `kubectl rollout pause deployment <deployment-name>` - Pause a specific deployment in the cluster.
- `kubectl rollout resume deployment <deployment-name>` - Resume a specific deployment in the cluster.
- `kubectl rollout restart deployment <deployment-name>` - Restart a specific deployment in the cluster.
- `kubectl set image deployment <deployment-name> <container-name>=<new-image-name>` - Update the image of a specific deployment in the cluster.
- `kubectl scale deployment <deployment-name> --replicas=<number-of-replicas>` - Scale a specific deployment in the cluster.
- `kubectl autoscale deployment <deployment-name> --min=<min-number-of-replicas> --max=<max-number-of-replicas> --cpu-percent=<cpu-percent>` - Autoscale a specific deployment in the cluster.
- `kubectl edit deployment <deployment-name>` - Edit a specific deployment in the cluster.
- `kubectl apply -f <deployment-file>` - Apply a specific deployment file to the cluster.
- `kubectl replace -f <deployment-file>` - Replace a specific deployment file in the cluster.

#### Deployment examples

- `kubectl create deployment nginx-deployment --image=nginx` - Create a new deployment with the image "nginx".
- `kubectl get deployments` - List all deployments in the cluster.
- `kubectl get deployment nginx-deployment` - List the deployment "nginx-deployment" in the cluster.

##### Example of a basic deployment file

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

##### Example of a basic deployment file with autoscaling

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
---
apiVersion: autoscaling/v1
kind: HorizontalPodAutoscaler
metadata:
  name: nginx-deployment
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: nginx-deployment
  minReplicas: 3
  maxReplicas: 10
  targetCPUUtilizationPercentage: 80
```

##### Example of a basic deployment file with liveness and readiness probes

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
        livenessProbe:
          httpGet:
            path: /
            port: 80
          initialDelaySeconds: 3
          periodSeconds: 3
        readinessProbe:
          httpGet:
            path: /
            port: 80
          initialDelaySeconds: 3
          periodSeconds: 3
```

##### Example of a basic deployment file with environment variables

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
        env:
        - name: ENV_VAR_NAME
          value: "env-var-value"
```

##### Example of a basic deployment file with secrets

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
        env:
        - name: SECRET_NAME
          valueFrom:
            secretKeyRef:
              name: secret-name
              key: secret-key
```

##### Example of a basic deployment file with configmaps

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
        env:
        - name: CONFIGMAP_NAME
          valueFrom:
            configMapKeyRef:
              name: configmap-name
              key: configmap-key
```

##### Example of a basic deployment file with volumes

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
        volumeMounts:
        - name: volume-name
          mountPath: /path/in/container
      volumes:
      - name: volume-name
        hostPath:
          path: /path/in/host
```

##### Example of a basic deployment file with persistent volumes and persistent volume claims

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
        volumeMounts:
        - name: volume-name
          mountPath: /path/in/container
      volumes:
      - name: volume-name
        persistentVolumeClaim:
          claimName: pvc-name
```

##### Example of a basic deployment file with service account and security context

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      serviceAccountName: service-account-name
      securityContext:
        runAsUser: 1000
        runAsGroup: 3000
        fsGroup: 2000
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

##### Example of a basic deployment file with node selectors and tolerations

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      nodeSelector:
        disktype: ssd
      tolerations:
      - key: "key"
        operator: "Equal"
        value: "value"
        effect: "NoSchedule"
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

##### Example of a basic deployment file with affinity and anti-affinity

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
            - matchExpressions:
              - key: kubernetes.io/e2e-az-name
                operator: In
                values:
                - e2e-az1
                - e2e-az2
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

##### Example of a basic deployment file with pod disruption budget

```yaml
apiVersion: policy/v1beta1
kind: PodDisruptionBudget
metadata:
  name: nginx-pdb
spec:
  minAvailable: 2
  selector:
    matchLabels:
      app: nginx
```

##### Example of a basic deployment file with pod priority and preemption

```yaml
apiVersion: scheduling.k8s.io/v1
kind: PriorityClass
metadata:
  name: high-priority
value: 1000000
globalDefault: false
description: "This priority class should be used for XYZ service only."
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  priorityClassName: high-priority
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

##### Example of a basic deployment file with pod security policy

```yaml
apiVersion: policy/v1beta1
kind: PodSecurityPolicy
metadata:
  name: restricted
spec:
  privileged: false
  allowPrivilegeEscalation: false
  requiredDropCapabilities:
  - ALL
  volumes:
  - 'configMap'
  - 'emptyDir'
  - 'projected'
  - 'secret'
  hostNetwork: false
  hostPorts:
  - min: 10000
    max: 11000
  hostIPC: false
  hostPID: false
  runAsUser:
    rule: 'RunAsAny'
  seLinux:
    rule: 'RunAsAny'
  supplementalGroups:
    rule: 'MustRunAs'
    ranges:
    - min: 1
      max: 65535
  fsGroup:
    rule: 'MustRunAs'
    ranges:
    - min: 1
      max: 65535
---
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: psp:restricted
rules:
- apiGroups:
  - policy
  resourceNames:
  - restricted
  resources:
  - podsecuritypolicies
  verbs:
  - use
---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: psp:restricted
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: Role
  name: psp:restricted
subjects:
- kind: ServiceAccount
  name: default
  namespace: default
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      securityContext:
        runAsUser: 1000
        runAsGroup: 3000
        fsGroup: 2000
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```
