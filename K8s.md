启动一个kubernetes集群 

> minikube start

删除一个kubrenetes集群,残留文件~/.minikube/目录下 

> minikube delete

获取minikube启动的虚拟机的ip

> Minikube ip –查看minikube所启动的虚拟机的ip, 该虚拟机网络模式是host-only模式

访问minikube内置的dashboard-UI 

> Minikube dashboard

登录到虚拟机内部 

> Minikube ssh 
> root@huzhengchuan-ThinkPad-T450:/home/huzhengchuan# minikube ssh

查看addons的列表 

> Minikube addons list 

启动某个addons 

> Minikube addons enable heapster

k8s获取服务

> kubectl get svc
>
> kubectl get service



kubectl run nginx --image=nginx:latest --replicas=3 --port=80



进入容器内部

	>kubectl exec nginx-app1-8677885866-6g2xz ps aux



```
kubectl get pod -o wide
```

minikube start --vm-driver=none --registry-mirror=https://registry.docker-cn.com

kubectl run hello-minikube --image=k8s.gcr.io/echoserver:1.4 --port=8080 

kubectl get pod











































K8s 部署 Nginx 入门

创建 pod
pod 是 k8s 最小的编排单位，通常来说不需要直接创建 pod。这里是为了演示 pod 的使用创建了一个 pod。

pod 的配置文件 nginx-pod.yml：

apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    app: nginx
spec:
  containers:
  - name: nginx
    image: nginx:alpine
    ports:
    - containerPort: 80
    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    其中配置项：

image：用于指定 nginx 容器使用的镜像
containerPort：容器内部监听端口，有关 k8s 各种 port 的使用，可以参考 链接
使用命令 kubectl apply 创建 pod：

kubectl apply -f nginx-pod.yml
1
为了检查创建的 pod 的状态，执行命令：

kubectl get pods nginx -o wide
1
可以看到 nginx pod 已处于 Running 状态，表示刚创建的 pod 已成功运行起来：

NAME    READY   STATUS    RESTARTS   AGE   IP          NODE             NOMINATED NODE   READINESS GATES
nginx   1/1     Running   0          69m   10.1.0.42   docker-desktop   <none>           <none>
1
2
如果需要显示更详细的 pod 的信息，可以使用命令：

kubectl describe pods nginx
1
为了进一步验证 nginx 已成功启动，进入 pod 中容器（有关如果进入 k8s 容器的命令介绍，可以参考 链接）：

kubectl exec -it nginx -- /bin/sh
1
进入容器后，执行命令：

curl localhost
1
可以正常打印出 nginx 启动成功的欢迎页面 html。

进行下面的实验前，可以先将刚创建的 pod 删除：

kubectl delete -f nginx-pod.yml
1
创建 deployment
k8s deployment 用来部署应用。一个常见的 deployment 配置包括几个部分，详细可以参考官网有关介绍 Deployments。

spec.selector：用于定义 deployment 如何查找要管理的 pod，例如，使用在 pod 模板中定义的标签，如 app:nginx
spec.replicas：用于定义需要启动多少个副本
spec.template：用于定义 pod 的属性，例如，容器名称，容器镜像，labels 字段，等
完整的 nginx-dep.yml 文件如下：

apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 3
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:alpine
        ports:
        - containerPort: 80
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
为了创建 deployment，执行命令：

kubectl apply -f nginx-dep.yml
1
查看 deployment 状态：

kubectl get deploy -o wide
1
可以看到，刚创建的 nginx-deployment 的 3 个副本均处于 READY 状态：

NAME               READY   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS   IMAGES         SELECTOR
nginx-deployment   3/3     3            3           48s   nginx        nginx:alpine   app=nginx
1
2
创建 service
k8s 使用 service 来实现服务发现，常见配置包括：

spec.selector：用于定义如何选择 pod
spec.ports：用于定义如何暴露端口，其中，nodePort 指定可以在外部访问的端口
完整的 nginx-svc.yml 文件如下：

apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
    nodePort: 30080
    type: NodePort
    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    为创建 servcie，执行命令：

kubectl apply -f nginx-svc.yml
1
查看 service 的状态：

kubectl get svc nginx-service -o wide
1
输出：

NAME            TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE   SELECTOR
nginx-service   NodePort   10.106.209.76   <none>        80:30080/TCP   26s   app=nginx
1
2
为了验证在外部正常访问 nginx，打开浏览器，输入地址 http://localhost:30080/，可以看到 nginx 的欢迎页面，说明 nginx-service 创建成功：