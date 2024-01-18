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

```bash
alias k=kubectl
```

### Erstellen der bind9 entries
### erstellen von ssh schl"ussel
### addend des ssh-keys zu agent
### Provisionierun des Clusters
```bash
vagrant up
```

```bash
cd kubespray && ansible-playbook -i inventory/k8s-cluster/hosts.yaml -u vagrant -b
```

### Operator Installieren
Installireung des Prometheus-Operators
```bash
LATEST=$(curl -s https://api.github.com/repos/prometheus-operator/prometheus-operator/releases/latest | jq -cr .tag_name)
curl -sL https://github.com/prometheus-operator/prometheus-operator/releases/download/${LATEST}/bundle.yaml | kubectl create -f -
```
Installierung des Grafana-Operators
### grafana
```bash
curl -sL https://github.com/operator-framework/operator-lifecycle-manager/releases/download/v0.26.0/install.sh | bash -s v0.26.0
```

```bash
kubectl create -f https://operatorhub.io/install/grafana-operator.yaml
```
### Grafan + Prometheus Loesung 

```bash
k apply -f observe.yaml
```
