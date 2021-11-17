# Exercices

## 2.01

https://github.com/pasiol/log-output/tree/2.01
https://github.com/pasiol/ping-pong/tree/2.01

    k3d cluster delete && k3d cluster create --port 8082:20080@agent:0 -p 8081:80@loadbalancer --agents 2 && docker exec k3d-k3s-default-agent-0 mkdir -p /tmp/kube

    kubectl apply -f https://raw.githubusercontent.com/pasiol/ping-pong/2.01/manifests/deploymentBusyBox.yaml
    pod/busybox1 created

    kubectl apply -f https://raw.githubusercontent.com/pasiol/ping-pong/2.01/manifests/deployment.yaml
    deployment.apps/ping-pong created
    kubectl apply -f https://raw.githubusercontent.com/pasiol/ping-pong/2.01/manifests/service.yaml
    service/ping-pong-svc created
    kubectl apply -f https://raw.githubusercontent.com/pasiol/ping-pong/2.01/manifests/ingress.yaml
    ingress.networking.k8s.io/ping-pong-ingress created

    kubectl get ing
    NAME                CLASS    HOSTS   ADDRESS                            PORTS   AGE
    ping-pong-ingress   <none>   *       172.19.0.2,172.19.0.4,172.19.0.5   80      55s

    kubectl get pods
    NAME                         READY   STATUS    RESTARTS   AGE
    busybox1                     1/1     Running   0          25m
    ping-pong-5d99cfc6cb-m9v9l   1/1     Running   0          24m

    kubectl exec -it ping-pong-5d99cfc6cb-m9v9l -- curl http://172.19.0.2/pingpong
    Ping / Pongs: 1

## 2.02

- https://github.com/pasiol/todo-project-backend/tree/2.02
- https://github.com/pasiol/todo-project/tree/2.02
- https://github.com/pasiol/to-do-project-frontend/tree/2.02

todo-project includes the builded version of React-frontend.

    kubectl get nodes -o wide
    NAME                       STATUS   ROLES                  AGE    VERSION        INTERNAL-IP   EXTERNAL-IP   OS-IMAGE   KERNEL-VERSION   CONTAINER-RUNTIME
    k3d-k3s-default-agent-1    Ready    <none>                 149m   v1.21.5+k3s2   172.18.0.3    <none>        Unknown    5.10.0-9-amd64   containerd://1.4.11-k3s1
    k3d-k3s-default-agent-0    Ready    <none>                 149m   v1.21.5+k3s2   172.18.0.4    <none>        Unknown    5.10.0-9-amd64   containerd://1.4.11-k3s1
    k3d-k3s-default-server-0   Ready    control-plane,master   150m   v1.21.5+k3s2   172.18.0.2    <none>        Unknown    5.10.0-9-amd64   containerd://1.4.11-k3s1

    sudo vim /etc/hosts

    127.0.0.1	localhost
    172.86.3.1	lab

    172.18.0.2 172.18.0.3 172.18.0.4 todo.local


    # The following lines are desirable for IPv6 capable hosts
    ::1     localhost ip6-localhost ip6-loopback
    ff02::1 ip6-allnodes
    ff02::2 ip6-allrouters

    kubectl apply -f https://raw.githubusercontent.com/pasiol/todo-project-backend/2.02/manifests/deployment.yaml
    deployment.apps/todo-project-backend created

    kubectl apply -f https://raw.githubusercontent.com/pasiol/todo-project-backend/2.02/manifests/service.yaml
    service/todo-project-backend-svc created
    kubectl get svc
    NAME                       TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE
    kubernetes                 ClusterIP   10.43.0.1       <none>        443/TCP    50m
    ping-pong-svc              ClusterIP   10.43.27.251    <none>        8888/TCP   46m
    todo-project-backend-svc   ClusterIP   10.43.175.225   <none>        8888/TCP   12s

    kubectl apply -f https://raw.githubusercontent.com/pasiol/todo-project-backend/2.02/manifests/toolbox.yaml
    pod/toolbox created

    kubectl exec -it toolbox -- curl -H "Content-Type: application/json" --request POST --data '{"task": "learn gorilla mux"}' http://10.43.175.225:8888/todos
    "new todo task created"

    kubectl get pods
    NAME                                    READY   STATUS    RESTARTS   AGE
    ping-pong-5d99cfc6cb-f9kl4              1/1     Running   0          64m
    todo-project-backend-5b99578688-5qptr   1/1     Running   0          18m
    toolbox                                 1/1     Running   0          12m
    busybox1                                1/1     Running   1          64m
    kubectl logs todo-project-backend-5b99578688-5qptr
    2021/11/16 19:52:36 Reading environment failed.
    2021/11/16 19:52:36 starting REST-backend in 0.0.0.0:8888.
    2021/11/16 19:52:36 Version: b7ab4c9989bf600f0d46c7912a0f6ee039167aaf , build: 2021-11-16T19:41:21+0000
    2021/11/16 19:52:36 Allowed origins: *
    2021/11/16 20:05:04 response bytes 4, []
    2021/11/16 20:10:06 response bytes 23, new todo task created

    kubectl apply -f https://raw.githubusercontent.com/pasiol/todo-project-backend/2.02/manifests/ingress.yaml
    ingress.networking.k8s.io/todo-project-backend-ingress created
    kubectl get ing
    NAME                           CLASS    HOSTS   ADDRESS                            PORTS   AGE
    ping-pong-ingress              <none>   *       172.18.0.2,172.18.0.3,172.18.0.4   80      66m
    todo-project-backend-ingress   <none>   *       172.18.0.2,172.18.0.3,172.18.0.4   80      8s
    kubectl delete ing ping-pong-ingress
    ingress.networking.k8s.io "ping-pong-ingress" deleted
    curl http://todo.local/todos
    [{"task":"learn gorilla mux"}]

    kubectl apply -f https://raw.githubusercontent.com/pasiol/todo-project/2.02/manifests/configMap.yaml
    configmap/web-config created
    kubectl apply -f https://raw.githubusercontent.com/pasiol/todo-project/2.02/manifests/persistentVolume.yaml
    persistentvolume/todo-project-pv created
    kubectl apply -f https://raw.githubusercontent.com/pasiol/todo-project/2.02/manifests/persistentVolumeClaim.yaml
    persistentvolumeclaim/todo-project-claim created
    kubectl apply -f https://raw.githubusercontent.com/pasiol/todo-project/2.02/manifests/deployment.yaml
    deployment.apps/todo-project created
    kubectl apply -f https://raw.githubusercontent.com/pasiol/todo-project/2.02/manifests/service.yaml
    service/todo-project-svc created
    kubectl apply -f https://raw.githubusercontent.com/pasiol/todo-project/2.02/manifests/ingress.yaml
    ingress.networking.k8s.io/todo-project-ingress created
    kubectl get pods
    NAME                                    READY   STATUS    RESTARTS   AGE
    ping-pong-5d99cfc6cb-f9kl4              1/1     Running   0          87m
    todo-project-backend-5b99578688-5qptr   1/1     Running   0          42m
    toolbox                                 1/1     Running   0          36m
    busybox1                                1/1     Running   1          87m
    todo-project-599dcd896-7gmf2            1/1     Running   0          26s
    kubectl logs todo-project-599dcd896-7gmf2
    2021/11/16 20:34:13 server started in port 3000
    2021/11/16 20:34:14 daily image getting statuscode 200
    2021/11/16 20:34:14 updated daily image succesfully

    firefox http://todo.local

![Screeshot](images/2.02.png)

## 2.03

- https://github.com/pasiol/ping-pong/tree/2.03
- https://github.com/pasiol/log-output/tree/2.03

cli:

    k3d cluster delete && k3d cluster create --port 8082:20080@agent:0 -p 8081:80@loadbalancer --agents 2 && docker exec k3d-k3s-default-agent-0 mkdir -p /tmp/kube
    kubectl create namespace applications
    kubectl config set-context --current --namespace=applications

    kubectl apply -f https://raw.githubusercontent.com/pasiol/ping-pong/2.03/manifests/deployment.yaml
    kubectl apply -f https://raw.githubusercontent.com/pasiol/ping-pong/2.03/manifests/service.yaml
    service/ping-pong-svc created
    kubectl apply -f https://raw.githubusercontent.com/pasiol/ping-pong/2.03/manifests/ingress.yaml
    ingress.networking.k8s.io/ping-pong-ingress created

    kubectl get ing
    NAME                CLASS    HOSTS   ADDRESS                            PORTS   AGE
    ping-pong-ingress   <none>   *       172.18.0.2,172.18.0.3,172.18.0.4   80      7m15s
    curl http://172.18.0.2/pingpong
    Ping / Pongs: 1

    kubectl apply -f https://raw.githubusercontent.com/pasiol/log-output/2.03/manifests/persistentVolume.yaml
    persistentvolume/log-output-pv created
    kubectl apply -f https://raw.githubusercontent.com/pasiol/log-output/2.03/manifests/persistentVolumeClaim.yaml
    persistentvolumeclaim/log-output-claim created
    kubectl apply -f https://raw.githubusercontent.com/pasiol/log-output/2.03/manifests/deployment.yaml
    deployment.apps/log-output-dep created
    kubectl apply -f https://raw.githubusercontent.com/pasiol/log-output/2.03/manifests/service.yaml
    service/log-output-svc created
    kubectl apply -f https://raw.githubusercontent.com/pasiol/log-output/2.03/manifests/ingress.yaml
    ingress.networking.k8s.io/log-output-ingress created

    NAME                 CLASS    HOSTS   ADDRESS                            PORTS   AGE
    ping-pong-ingress    <none>   *       172.18.0.2,172.18.0.3,172.18.0.4   80      16m
    log-output-ingress   <none>   *       172.18.0.2,172.18.0.3,172.18.0.4   80      36s
    curl http://172.18.0.2
    2021-11-17T14:30:49.893084222Z 177e215e-1252-4b09-8256-02aea10703cb
    Ping / Pongs: 2

## 2.04

- https://github.com/pasiol/todo-project/tree/2.04
- https://github.com/pasiol/todo-project-backend/tree/2.04

cli:

    kubectl delete ing ping-pong-ingress
    ingress.networking.k8s.io "ping-pong-ingress" deleted
    kubectl delete ing log-output-ingress
    ingress.networking.k8s.io "log-output-ingress" deleted

    kubectl create namespace todo-project
    namespace/todo-project created
      kubectl config set-context --current --namespace=todo-project
    Context "k3d-k3s-default" modified.

    kubectl apply -f https://raw.githubusercontent.com/pasiol/todo-project-backend/2.04/manifests/deployment.yaml
    deployment.apps/todo-project-backend created
    kubectl apply -f https://raw.githubusercontent.com/pasiol/todo-project-backend/2.04/manifests/service.yaml
    service/todo-project-backend-svc created
    kubectl apply -f https://raw.githubusercontent.com/pasiol/todo-project-backend/2.04/manifests/ingress.yaml
    ingress.networking.k8s.io/todo-project-backend-ingress created

    kubectl get ing
    NAME                           CLASS    HOSTS   ADDRESS                            PORTS   AGE
    todo-project-backend-ingress   <none>   *       172.18.0.2,172.18.0.3,172.18.0.4   80      11s

    curl -H "Content-Type: application/json" --request POST -d '{"task": "learn golang"}' http://todo.local/todos
    "new todo task created"
    curl http://todo.local/todos
    [{"task":"learn golang"}]

    kubectl apply -f https://raw.githubusercontent.com/pasiol/todo-project/2.04/manifests/configMap.yaml
    configmap/web-config created
    kubectl apply -f https://raw.githubusercontent.com/pasiol/todo-project/2.04/manifests/persistentVolume.yaml
    persistentvolume/todo-project-pv created
    kubectl apply -f https://raw.githubusercontent.com/pasiol/todo-project/2.04/manifests/persistentVolumeClaim.yaml
    persistentvolumeclaim/todo-project-claim created
    kubectl apply -f https://raw.githubusercontent.com/pasiol/todo-project/2.04/manifests/deployment.yaml
    deployment.apps/todo-project created
    kubectl apply -f https://raw.githubusercontent.com/pasiol/todo-project/2.04/manifests/service.yaml
    service/todo-project-svc created
    kubectl apply -f https://raw.githubusercontent.com/pasiol/todo-project/2.04/manifests/ingress.yaml
    ingress.networking.k8s.io/todo-project-ingress created
    kubectl get ing
    NAME                           CLASS    HOSTS   ADDRESS                            PORTS   AGE
    todo-project-backend-ingress   <none>   *       172.18.0.2,172.18.0.3,172.18.0.4   80      12m
    todo-project-ingress           <none>   *       172.18.0.2,172.18.0.3,172.18.0.4   80      9s

    firefox http://todo.local

![Screeshot](images/2.04.png)
