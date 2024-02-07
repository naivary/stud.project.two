## Vorrausetzung
Für die erfolgreiche Provisionierung des Kubernetes-Produktionsclusters müssen folgende Vorrausetzungen erfüllt sein:
- Ubuntu Betriebssystem (mindestens Version 20.04)
- [Oracle VirtualBox](https://www.virtualbox.org/wiki/Downloads) installiert auf dem Ubuntu System
- [Vagrant](https://developer.hashicorp.com/vagrant/downloads#Linux) installiert auf dem Ubuntu System

## Installation von Software-Pakete und Aktualisierung von Ubuntu
Zuerst müssen die Packages von Ubuntu aktualisiert werden und benötigte Software-Pakete installiert werden. Zu den benötigten Software-Paketen gehöhren:
- jq
- haproxy
- python3.11
- kubectl

Für das einfache arbeiten mit dem CLI von Kubernetes wird ebenfalls ein alias `k` gesetz für das Kommando `kubectl`
```bash
sudo apt-get update -y
```

```bash
sudo apt-get upgrade -y
```

```bash
sudo apt install haproxy jq -y
```

```bash
sudo add-apt-repository ppa:deadsnakes/ppa -y && sudo apt update -y
```

```bash
sudo apt install python3.11 -y && sudo apt install python3.11-venv -y
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

### Klonen des Git-Repositories
Im Git-Repositorie sind bereits einige Vorkehrungen getroffen wurden, für einfache Provisionierung des Kubernetes-Produktionsclusters und die Interaktion mit diesem. Zu den Vorkehrung gehören beispielsweise:
- Das Definieren des Ansible Inventories
- Das Definieren des Vagrantfiles für die Infrastruktur Provisionierung
- Das Definieren des haproxy Config-Datei

```bash
git clone https://github.com/naivary/stud.project.two.git && cd stud.project.two
```

### Provisionierung der Infrastruktur mithilfe von Vagrant
Im Folgendem werden insgesamt 5 virtuelle Maschinen provisioniert (3 Control Planes und 2 Nodes). Ebenfalls wird eine Python Virtual Environment erstellt, für die Installation der Kubespray [Abhängigkeit](./kubespray/requirements.txt)
```bash
vagrant up
```

```bash
python3.11 -m venv .va
```

```bash
. .va/bin/activate
```

```bash
cd kubespray && pip install -r requirements.txt
```

```bash
ansible-playbook -i inventory/k8s-cluster/hosts.yaml -u vagrant -b cluster.yml
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
sudo chown vagrant:vagrant admin.conf
```

```bash
exit
```

```bash
scp vagrant@192.168.56.61:/home/vagrant/admin.conf ~/.kube/config
```

```bash
sudo cp haproxy.cfg /etc/haproxy/haproxy.cfg && sudo systemctl restart haproxy
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
cd .. && k apply -f observe.yaml
```

Das Grafana dashboard sollt ein kuerze unter der Adresse https://192.168.56.200 erreichbar sein. 

Die Anmeldedaten sind:
Username: root
Password: secret
