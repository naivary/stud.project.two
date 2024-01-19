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
sudo add-apt-repository ppa:deadsnakes/ppa -y && sudo apt update && sudo apt install python3.11 && sudo apt install python3.11-venv -y
```

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```

```bash
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
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

```bash
sudo apt install haproxy && sudo cp haproxy.cfg /etc/haproxy/haproxy.cfg && sudo systemctl restart haproxy
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

### Copy the kubeconfig
```bash
mkdir ~/.kube
```

```bash
ssh vagrant@192.168.56.61
```

```bash
sudo cp /etc/kubernetes/admin.conf admin.conf
```

```bash
sudo chown vagrant:vagrant amdin.conf
```

```bash
exit
```

```bash
scp vagrant@192.168.56.61:/home/vagrant/admin.conf ~/.kube/config
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
