## Vorrausetzung
Für die erfolgreiche Provisionierung des Kubernetes-Produktionsclusters müssen folgende Voraussetzungen erfüllt sein:
- Ubuntu Betriebssystem (mindestens Version 20.04)
- [Oracle VirtualBox](https://www.virtualbox.org/wiki/Downloads) installiert auf dem Ubuntu System
- [Vagrant](https://developer.hashicorp.com/vagrant/downloads#Linux) installiert auf dem Ubuntu System

## Installation und Aktualisierung
Zuerst müssen die bereits vorhandenen Softwarepakete aktualisiert und benötigte installiert werden. Zu den benötigten Softwarepaketen gehören:
- jq
- haproxy
- python3.11
- kubectl

Für das einfache Arbeiten mit dem CLI von Kubernetes wird ein Alias `k` für das Kommando `kubectl` gesetzt.
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
Im Git-Repository wurden bereits einige Vorkehrungen für die einfache Provisionierung des Kubernetes-Produktionsclusters und die Interaktion damit getroffen. Zu den Vorkehrungen gehören beispielsweise:
- Das Definieren des Ansible-Inventories.
- Das Festlegen des Vagrantfiles für die Infrastrukturprovisionierung.
- Das Erstellen der haproxy-Konfigurationsdatei.

```bash
git clone https://github.com/naivary/stud.project.two.git && cd stud.project.two
```

### Provisionierung der Infrastruktur mithilfe von Vagrant
Im Folgendem werden insgesamt 5 virtuelle Maschinen provisioniert (3 Control Planes und 2 Nodes). Ebenfalls wird eine Python Virtual Environment erstellt, für die Installation der Kubespray [Abhängigkeiten](./kubespray/requirements.txt). Im Vagranfile sollte das richtige Bridge Netzwerk eingestellt werden.

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

### Kopieren der Kubernetes-Konfiguration
Damit die Interaktion zwischen dem Ubuntu-Infrakstruktursystem und dem Kubernetes-Produktionscluster gelingt, muss die Kubernetes-Konfiguration `kubectl` bekannt sein. Diese ist bereits auf einem der drei Control Planes vordefiniert und muss ausschließlich auf das Infrastruktursystem kopiert werden. Der `.kube`-Ordner im Homeverzeichnis des aktuellen Ubuntu-Nutzers ist der Standardordner von `kubectl`. Dort erwartet `kubectl` die Kubernetes-Konfiguration.

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

### Implementierung der beispielhaften Observability-Lösung
Für die Implementierung der beispielhaften Observability-Lösung werden die beiden Kubernetes-Operatoren Prometheus-Operator und Grafana-Operator benötigt.

```bash
LATEST=$(curl -s https://api.github.com/repos/prometheus-operator/prometheus-operator/releases/latest | jq -cr .tag_name)
curl -sL https://github.com/prometheus-operator/prometheus-operator/releases/download/${LATEST}/bundle.yaml | kubectl create -f -
```

```bash
curl -sL https://github.com/operator-framework/operator-lifecycle-manager/releases/download/v0.26.0/install.sh | bash -s v0.26.0
```

```bash
kubectl create -f https://operatorhub.io/install/grafana-operator.yaml
```

### Deployment der beispielhaften Lösung
In der `observe.yaml` Datei werden die Kubernetes-Objekte definiert, die für die beispielhafte Lösung benötigt werden. Sollte ein Fehler auftreten, sollte das zweite Kommando ausgeführt werden, bis Erfolg verzeichnet wird. Die Fehler können aufgrund der Abhängigkeiten der Kubernetes-Objekte entstehen, die möglicherweise noch nicht vollständig erstellt wurden.

```bash
cd ..
```

```bash
k apply -f observe.yaml
```

### Zugriff auf das Grafana-Dashboard
Das Grafana-Dashboard kann nach erfolgreichem Deployment unter der Adresse https://192.168.56.200 erreicht werden. Die Anmeldeinformationen lauten wie folgt:
- Username: root
- Password: secret
