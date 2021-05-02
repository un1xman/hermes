# Hermes
### Hermes was the reporter god in Greek mythology but here is just a DevOps tool

Installation of Prometheus Grafana and Metrics Servers to Kuberetes via Ansible

#### Prerequisites:
Connection with Destination Kubernetes via kubectl on local or Jenkins Node

#### Requirments:
| Tech | Version |
| ------ | ------ |
| Kubernetes | v1.19+ |
| Ansible | 2.9.6 |
| Ansible-Galaxy | 2.9.6 |
| Helm | 3.x | 


##### Prometheus Helm Parameteres

 Parameter                  | Description                                                          | Default                                                 |
|---------------------------|----------------------------------------------------------------------|---------------------------------------------------------|
| `obectName`               | Name of Service, Pod Selector app                                    | `prometheus`                                            |
| `replicaCount`            | Deployment Replica count                                             | `1`                                                     |
| `ImageName`               | Image address of Prometheus                                          | `prom/prometheus`                                       |
| `containerPort`           | Port of Prometheus container                                         | `9090`                                                  |
| `service.type`            | K8s Service type                                                     | `ClusterIP`                                             |
| `service.port`            | Service Port                                                         | `80`                                                    |
| `ingress.enabled`         | Ingress status                                                       | `true`                                                  |
| `ingres.hostname`         | Prometheus domain                                                    | `nil`                                                   |  
| `ingress.annotaions`      | Ingress annotations                                                  | `[]`                                                    |
| `pvc.name`                | Grafana data pvc name                                                | `grafana`                                               |
| `pvc.accessMode`          | Access mode of PVC                                                   | `ReadWriteOnce`                                         |
| `storageSize`             | Capacity of PVC                                                      | `5G`                                                    |
| `storageclassname`        | Storageclass name on Kubernetes                                      | `[]`                                                       | 

##### Grafana Helm Parameteres

Parameter                  | Description                                                          | Default                                                 |
|---------------------------|----------------------------------------------------------------------|---------------------------------------------------------|
| `obectName`               | Name of Service, Pod Selector app                                    | `grafana`                                               |
| `replicaCount`            | Deployment Replica count                                             | `1`                                                     |
| `ImageName`               | Image address of Prometheus                                          | `grafana/grafana:latest`                                |
| `containerPort`           | Port of Prometheus container                                         | `3000`                                                  |
| `service.type`            | K8s Service type                                                     | `ClusterIP`                                             |
| `service.port`            | Service Port                                                         | `80`                                                    |
| `ingress.enabled`         | Ingress status                                                       | `true`                                                  |
| `ingres.hostname`         | Prometheus domain                                                    | `nil`                                                   |  
| `ingress.annotaions`      | Ingress annotations                                                  | `[]`                                                    |
| `pvc.name`                | Grafana data pvc name                                                | `grafana`                                               |
| `pvc.accessMode`          | Access mode of PVC                                                   | `ReadWriteOnce`                                         |
| `storageSize`             | Capacity of PVC                                                      | `5G`                                                    |
| `storageclassname`        | Storageclass name on Kubernetes                                      | `[]`                                                    | 


Installation

```bash
ansible-playbook playbook.yaml -e KUBECONFIG="/path/kubeconfig"
```
##### Prometheus Helm Chart Version: 0.1.0
##### Grafana Helm Chart Version: 0.1.0

Separately Installtion of Components

- Prometheus
    ```bash
    helm install -n monitoring prometheus -f k8s/prometheus-helm-template/values.yaml k8s/prometheus-helm-template
    ```
- Grafana
    ```bash
    helm install -n monitoring grafana -f k8s/grafana-helm-template/values.yaml k8s/grafana-helm-template
    ```
- Metrics Server
    ```bash
    kubectl apply -f k8s/metric-server/metric-server-manifest.yaml
    ```

### ✨Happy Coding✨

(C)un1xman
