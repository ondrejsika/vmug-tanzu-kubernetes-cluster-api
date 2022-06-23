# VMUG: Tanzu Kubernetes Cluster API

Login

```
kubectl vsphere login --server=tanzu-cra.sikademo.com --vsphere-username ondrej.sika --insecure-skip-tls-verify
```

Use context

```
kubectl config use-context tanzu-cra.sikademo.com
```

Set namespace

```
kubectl config set-context --current --namespace sikalabs
```

List all Kubernete API resources

```
kubectl api-resources
```

List Tanzu resources

```
kubectl api-resources | grep run.tanzu.vmware.com
```

```
kubectl api-resources | grep vmoperator.vmware.com
```

List Cluster API resources

```
kubectl api-resources | grep x-k8s.io
```

List Tanzu Kubernetes Releases

```
kubectl get tkr
```

List Tanzu Addons

```
kubectl get tka
```

List Tanzu clusters

```
kubectl get tkc
```

Create cluster

```
kubectl apply -f tkc-foo-v1.yml
```

List clusters again

```
kubectl get tkc
```

List VMs

```
kubectl get vm
```

List Cluster API clusters

```
kubectl get cl
```

Machine deployments

```
kubectl get md
```

Machines

```
kubectl get ma
```

Wait until cluster will be running

```
kubectl wait --for=jsonpath='{.status.phase}'=running tkc/foo
```

Get `kubeconfig.yml`

```
kubectl get secret foo-kubeconfig --output jsonpath="{.data.value}" | base64 --decode > kubeconfig-foo.yml
```

Add node to `foo` cluster

```
vimdiff tkc-foo-v1.yml tkc-foo-v2.yml
```

Apply

```
kubectl apply -f tkc-foo-v2.yml
```

```
kubectl get tkc
```

```
kubectl wait --for=jsonpath='{.status.phase}'=running tkc/foo
```

```
kubectl get tkc
```

Add more masters

```
vimdiff tkc-foo-v2.yml tkc-foo-v3.yml
```

```
kubectl apply -f tkc-foo-v3.yml
```


Connect to cluster

```
export KUBECONFIG=kubeconfig-foo.yml
```

Apply policy

```
kubectl create clusterrolebinding default-tkg-admin-privileged-binding --clusterrole=psp:vmware-system-privileged --group=system:authenticated
```

Test cluster

```
helm repo add sikalabs https://helm.sikalabs.io
```

```
helm install --upgrade hello sikalabs/hello-world
```

```
kubectl get all
```

```
kubectl port-forward svc/hello 8000:80
```

See: http://127.0.0.1:8000

Update `hello` service to LoadBalancer

```
kubectl edit svc hello
```

Get svc hello

```
kubectl get svc hello
```

Check the public IP

Create Tanzu cluster using Helm

See manifests

```
helm template bar ./charts/tkc --values bar-global.values.yml
```

Install

```
helm upgrade --install bar ./charts/tkc --values bar-global.values.yml
```

List Tanzu clusters

```
kubectl get tkc
```

```
kubectl get tkc,vm,cl,md,ma
```

```
kubectl get tkc
kubectl get vm
kubectl get cl
kubectl get md
kubectl get ma
```

Update cluster

See the diff

```
vimdiff <(helm template bar ./charts/tkc --values bar-global.values.yml) <(helm template bar ./charts/tkc --values bar-global.values.yml --values bar-v2.values.yml)
```

Update

```
helm upgrade --install bar ./charts/tkc --values bar-global.values.yml --values bar-v2.values.yml
```
