# operator-sdk (helm-based)

https://sdk.operatorframework.io/docs/building-operators/helm/quickstart/

## Steps

```
mkdir nginx-operator
cd nginx-operator
operator-sdk init --domain example.com --plugins helm
```

```
operator-sdk create api --group demo --version v1alpha1 --kind Nginx
```

```
make docker-build docker-push IMG="nakamasato/nginx-operator:v0.0.1"
```

Deploy operator

```
make deploy IMG="nakamasato/nginx-operator:v0.0.1"
```

```
kubectl get deploy -n nginx-operator-system
NAME                                READY   UP-TO-DATE   AVAILABLE   AGE
nginx-operator-controller-manager   1/1     1            1           25s
```

Create a sample Nginx custom resource

```
kubectl apply -f config/samples/demo_v1alpha1_nginx.yaml
```

```
kubectl get Nginx nginx-sample
NAME           AGE
nginx-sample   34s
```

```
kubectl get deploy
NAME           READY   UP-TO-DATE   AVAILABLE   AGE
nginx-sample   0/1     1            0           14s
```

undeploy

```
make undeploy
```
