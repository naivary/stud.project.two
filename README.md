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
sudo apt install python3-venv -y
```

```bash
alias k=kubectl
```

### Generieren eines Schluesselpaars
```bash
ssh-keygen -t rsa -b 2048
```

### Klonen des Projektes
```bash
git clone https://github.com/naivary/stud.project.two.git
```

```bash
cd stud.project.two
```

### Provisionierung des Clusters
```bash
vagrant up
```

```bash
python3 -m venv .va
```

```bash
. .va/bin/activate
```

```bash
cd kubespray && pip install -r requirements.txt
```

```bash
ansible-playbook -i inventory/k8s-cluster/hosts.yaml -u vagrant -b
```

### Operator Installieren
Installireung des Prometheus-Operators
```bash
LATEST=$(curl -s https://api.github.com/repos/prometheus-operator/prometheus-operator/releases/latest | jq -cr .tag_name)
curl -sL https://github.com/prometheus-operator/prometheus-operator/releases/download/${LATEST}/bundle.yaml | kubectl create -f -
```
Installierung des Grafana-Operators
### Grafana
```bash
curl -sL https://github.com/operator-framework/operator-lifecycle-manager/releases/download/v0.26.0/install.sh | bash -s v0.26.0
```

```bash
kubectl create -f https://operatorhub.io/install/grafana-operator.yaml
```
### Grafana + Prometheus Loesung 

```bash
k apply -f observe.yaml
```
