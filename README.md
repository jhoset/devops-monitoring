# 📊 Proyecto DevOps Monitoring – AKS + Prometheus + Grafana + Loki

## 👤 Autor
**Jhoset Nina**  
Curso: *DevOps Monitoring*  
Módulo: *Monitoreo y Observabilidad*  

---

## 🎯 Objetivo del proyecto

Implementar una **solución básica de monitoreo y observabilidad** sobre Kubernetes en Azure, reutilizando los conceptos vistos en clase, para:

- Desplegar infraestructura como código con **Terraform**
- Ejecutar una **aplicación Node.js simple (Hello World)**
- Monitorear métricas del clúster y la aplicación con **Prometheus**
- Visualizar métricas y logs con **Grafana**
- Generar **alertas automáticas** y enviarlas por **correo electrónico**
- Centralizar logs usando **Loki + Promtail**

El proyecto se enfoca en un **MVP funcional**, sin complejidad innecesaria.

---

## 🧱 Arquitectura general

**Componentes del proyecto:**

- Azure Kubernetes Service (AKS)
- Terraform
- Node.js API
- Prometheus
- Alertmanager
- Grafana
- Loki + Promtail

---

## 📂 Estructura del repositorio

```text
devops_monitoring/
├── Clase_01_02/
│   ├── aks.tf
│   ├── node-deployment.yaml
│   ├── node-service.yaml
│   ├── values.yaml
│   └── alerts/
│       ├── disk-alerts.yaml
│       └── memory-alerts.yaml
└── README.md
```

---

## ⚙️ Requisitos previos

- Cuenta en Azure
- Azure CLI
- Terraform
- kubectl
- Helm
- Docker Hub (imagen Node.js)

---

## 🚀 Infraestructura con Terraform

```bash
terraform init
terraform apply
```

---

## 🔐 Acceso al clúster AKS

```bash
az aks get-credentials   --resource-group rg-jhosetnina-dev-eastus-01   --name aks-jhosetnina-dev-eastus-01   --overwrite-existing
```

---

## 📦 Namespace de monitoreo

```bash
kubectl create namespace monitoring
```

---

## 📈 Prometheus

```bash
helm install prometheus prometheus-community/prometheus   --namespace monitoring
```

---

## 📊 Grafana

```bash
helm install grafana grafana/grafana   --namespace monitoring
```

---

## 🌐 Aplicación Node.js

```bash
kubectl apply -f node-deployment.yaml
kubectl apply -f node-service.yaml
```

---

## 🚨 Alertas

Las alertas de uso de disco y memoria están configuradas en `values.yaml` y se envían por correo electrónico usando Alertmanager.

---

## 🔥 Simulación de alerta

```bash
kubectl run disk-test --rm -i --tty --image=ubuntu -- bash
dd if=/dev/zero of=file1 bs=1M count=1000
```

---

## 📝 Logs con Loki

```bash
helm upgrade --install loki grafana/loki-stack   --namespace monitoring   --set grafana.enabled=false   --set promtail.enabled=true
```

Datasource en Grafana:

```text
http://loki:3100
```

---

## ✅ Resultados

✔ AKS operativo  
✔ App Node.js desplegada  
✔ Métricas y logs visibles  
✔ Alertas enviadas por correo  

---

## 🧠 Conclusión

El proyecto demuestra una implementación realista y funcional de monitoreo en Kubernetes, alineada a las buenas prácticas DevOps.
