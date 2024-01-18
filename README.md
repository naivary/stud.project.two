## Vorrausetzung
Es wird ein Ubuntu (20.04) benoetigt.
## Vorgehen fuer das Deployment des k8s Clusters.
```bash
sudo apt-get update -y
```

```bash
sudo apt-get upgrade -y
```

```bash
sudo apt install bind9 bind9utils bind9-doc -y
```




### Erstellen der bind9 entries
### erstellen von ssh schl"ussel
### addend des ssh-keys zu agent
### vagrant up
### ansible-playbook -i inventory/k8s-cluster/hosts.yaml
### nginx controller
```bash
k apply -f ingress/controller/nginx.yaml
```
### metallb deploy -> l2 -> ippool
```bash
k apply -f deploy.yaml && k apply -f l2advertisment.yaml && k apply -f ip-pool.yaml
```
### prometheus
```bash
LATEST=$(curl -s https://api.github.com/repos/prometheus-operator/prometheus-operator/releases/latest | jq -cr .tag_name)
curl -sL https://github.com/prometheus-operator/prometheus-operator/releases/download/${LATEST}/bundle.yaml | kubectl create -f -
```

```bash
k apply -f rbac.yaml
k apply -f prometheus.yaml
k apply -f kubelet_job.yaml
k apply -f cadvisor_job.yaml
```
### grafana
```bash
curl -sL https://github.com/operator-framework/operator-lifecycle-manager/releases/download/v0.26.0/install.sh | bash -s v0.26.0
```

```bash
kubectl create -f https://operatorhub.io/install/grafana-operator.yaml
```

```bash
k apply -f grafana.yaml
k apply -f prometheus_datasource.yaml
k apply -f ingress_rule.yaml
```
