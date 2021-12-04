# Exercices

## 4.01

- https://github.com/pasiol/ping-pong/tree/exercise401
- https://github.com/pasiol/log-output/tree/exercise401

pingpong-deployment jää jumiin puuttuneen pvc:n takia (kommentoitu kustomizion filessä). Se ajetaan konsolista manuaalisesti alla myöhemmin.

- https://github.com/pasiol/ping-pong/actions/runs/1538870127
- https://github.com/pasiol/log-output/actions/runs/1539176462


    kubectl config set-context --current --namespace=exercise401

    kubectl get pods

    NAME                                  READY   STATUS    RESTARTS   AGE
    log-output-dep-dfc6d5945-bwtpq        1/2     Running   0          4m21s
    ping-pong-799b5868b5-27srr            0/1     Running   0          10m
    ping-pong-postgres-5ff5f79966-9ptz5   0/1     Pending   0          10m

    kubectl apply -f tmp/pvc.yaml
    persistentvolumeclaim/pingpong-pvc created

    kubectl get pods

    NAME                                  READY   STATUS    RESTARTS   AGE
    log-output-dep-dfc6d5945-bwtpq        1/2     Running   0          5m9s
    ping-pong-799b5868b5-27srr            0/1     Running   0          11m
    ping-pong-postgres-5ff5f79966-9ptz5   0/1     Pending   0          11m

    kubectl get pods

    NAME                                  READY   STATUS    RESTARTS   AGE
    log-output-dep-dfc6d5945-bwtpq        1/2     Running   0          5m33s
    ping-pong-799b5868b5-27srr            0/1     Running   0          11m
    ping-pong-postgres-5ff5f79966-9ptz5   1/1     Running   0          11m

    kubectl get pods
    NAME                                  READY   STATUS              RESTARTS      AGE
    log-output-dep-dfc6d5945-bwtpq        1/2     Running             0             6m10s
    ping-pong-799b5868b5-27srr            1/1     Running             1 (25s ago)   12m
    ping-pong-799b5868b5-6znr8            0/1     ContainerCreating   0             1s
    ping-pong-postgres-5ff5f79966-9ptz5   1/1     Running             0             12m

    kubectl get pods

    NAME                                  READY   STATUS    RESTARTS      AGE
    log-output-dep-dfc6d5945-bwtpq        2/2     Running   0             6m43s
    ping-pong-799b5868b5-27srr            1/1     Running   1 (58s ago)   12m
    ping-pong-799b5868b5-6znr8            1/1     Running   0             34s
    ping-pong-postgres-5ff5f79966-9ptz5   1/1     Running   0             12m

    kubectl get ing

    NAME                   CLASS    HOSTS   ADDRESS        PORTS   AGE
    applications-ingress   <none>   *       34.96.64.155   80      7m51s

    curl http://34.96.64.155/health
    {"message":"ok"}

    curl http://34.96.64.155/

    <pre>Hello
    2021-12-04T15:45:19.491421667Z c8c5e457-9d1a-4292-a44a-d09b36256c8c
    Ping / Pongs: 32
    </pre>

    kubectl get svc
    NAME                     TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
    log-output-svc           NodePort    10.32.1.25    <none>        80:30405/TCP   8m51s
    ping-pong-postgres-svc   ClusterIP   10.32.1.255   <none>        5432/TCP       14m
    ping-pong-svc            ClusterIP   10.32.14.24   <none>        80/TCP         14m

    kubectl apply -f tmp/toolbox.yaml
    pod/toolbox created

    kubectl exec toolbox -- curl http://10.32.14.24/health

    {"message":"ok"}

    kubectl exec toolbox -- curl http://10.32.14.24/pingpong

    Ping / Pongs: 60
