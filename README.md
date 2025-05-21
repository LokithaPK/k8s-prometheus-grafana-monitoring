# Kubernetes Monitoring with Prometheus and Grafana

This project sets up a monitoring solution for a Kubernetes cluster using Prometheus for metrics collection and Grafana for visualization.

## 🔧 Tools Used
- Kubernetes   (Minikube for local cluster)
- Prometheus  – for scraping metrics
- Grafana     – for visualization
- Helm        – for package management

## 🛠️ Setup Instructions

### 1. Start Minikube

minikube start

### 2.Install Prometheus

helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install prometheus prometheus-community/prometheus
kubectl expose service prometheus-server --type=NodePort --target-port=9090 --name=prometheus-server-ext

### 3. Install Grafana

helm repo add grafana https://grafana.github.io/helm-charts
helm repo update
helm install grafana grafana/grafana
kubectl get secret --namespace default grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
kubectl expose service grafana --type=NodePort --target-port=3000 --name=grafana-ext
