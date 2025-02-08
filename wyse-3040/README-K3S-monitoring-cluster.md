# K3S Cluster with Dell Wyse 3040 Thin Clients

## Setup Steps

### 1. Prepare BIOS & USB Boot

- Ensure BIOS allows USB booting.
- Create Alpine Linux USB stick:
    
    ```sh
    sudo dd if=alpine-standard-3.20.3-x86_64.iso of=/dev/sdX bs=4M status=progress oflag=sync
    ```
    
    _(Replace `/dev/sdX` with your actual USB device)_

### 2. Install Alpine Linux

- Boot from USB and install using `setup-alpine`.
- (Optional) Use Ansible to automate installation.

### 3. Configure Shared Mount

- Create a script on all nodes:
    
    ```sh
    sudo vim /etc/local.d/make-shared.start
    ```
    
    **Add the following lines:**
    
    ```sh
    mount --make-shared / && mount -o remount /
    ```
    
    - Make the script executable:
        
        ```sh
        sudo chmod +x /etc/local.d/make-shared.start
        ```
        

### 4. Install K3S

- Follow the [K3S Quick Start Guide](https://docs.k3s.io/quick-start).
- **Master Node Installation:**
    
    ```sh
    curl -sfL https://get.k3s.io | sh -
    ```
    
    - The kubeconfig file will be available at:
        
        ```
        /etc/rancher/k3s/k3s.yaml
        ```
        
- **Worker Node Installation:**
    
    ```sh
    curl -sfL https://get.k3s.io | K3S_URL=https://<master-ip>:6443 K3S_TOKEN=<node-token> sh -
    ```
    

### 5. Install Management Tools

#### Install k9s

```sh
sudo wget https://github.com/derailed/k9s/releases/download/v0.32.7/k9s_linux_amd64.deb
sudo apt install ./k9s_linux_amd64.deb
rm k9s_linux_amd64.deb
```

#### Install kubectl

```sh
sudo apt-get update && sudo apt-get install -y kubectl
```

- Verify setup:
    
    ```sh
    mkdir -p ~/.kube
    kubectl config view
    kubectl config get-contexts
    ```
    

#### Connect k9s to K3S Cluster

- Copy the kubeconfig file from the master node to your host machine:
    
    ```sh
    scp user@<master-ip>:/etc/rancher/k3s/k3s.yaml ~/.kube/config
    ```
    
- Update the kubeconfig file to use the correct master node IP:
    
    ```sh
    sed -i 's/127.0.0.1/<master-ip>/g' ~/.kube/config
    ```
    
- Verify k9s can access the cluster:
    
    ```sh
    kubectl get nodes
    k9s
    ```
    

### 6. Install Helm and Deploy Example Prometheus Stack

#### Install Helm

```sh
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```

- Add Helm repositories:
    
    ```sh
    helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
    helm repo update
    ```
    

#### Install NFS Provisioner

```sh
helm repo add nfs-subdir-external-provisioner https://kubernetes-sigs.github.io/nfs-subdir-external-provisioner/
helm repo update
helm install nfs-client-provisioner nfs-subdir-external-provisioner/nfs-subdir-external-provisioner -f values.yaml
```

#### Deploy Prometheus Stack

- **Apply Grafana Admin Secret:**
    
    ```sh
    kubectl apply -f secrets.yaml
    ```
    
- **Create `secrets.yaml` for Grafana credentials:**
    
    ```yaml
    apiVersion: v1
    kind: Secret
    metadata:
      name: grafana-admin
      namespace: monitoring
    stringData:
      username: grafana-admin
      password: password
    ```
    
- **Create `values.yaml` for Prometheus & Grafana configuration:**
    
    ```yaml
    prometheus:
      service:
        type: NodePort
        nodePort: 30001
      enabled: true
      prometheusSpec:
        storageSpec:
          volumeClaimTemplate:
            spec:
              storageClassName: nfs-client
              accessModes:
                - ReadWriteOnce
              resources:
                requests:
                  storage: 1Gi
        retention: 365d
        additionalScrapeConfigs:
          - job_name: "pi"
            static_configs:
              - targets: ["192.168.2.229:9101"]
    
    grafana:
      persistence:
        type: pvc
        storageClassName: nfs-client
        enabled: true
        size: 1Gi
      admin:
        existingSecret: grafana-admin
        userKey: username
        passwordKey: password
      service:
        type: NodePort
        nodePort: 30000
    
    alertmanager:
      enabled: true
      service:
        type: NodePort
        nodePort: 30002
    ```
    
- **Install Prometheus and Grafana:**
    
    ```sh
    helm install kube-prometheus prometheus-community/kube-prometheus-stack -n monitoring --create-namespace -f values.yaml
    ```
    
- **To upgrade or reinstall Prometheus stack:**
    
    ```sh
    helm upgrade --install kube-prometheus prometheus-community/kube-prometheus-stack -n monitoring --create-namespace -f values.yaml
    ```
    
- **To delete and reinstall the monitoring stack:**
    
    ```sh
    helm uninstall kube-prometheus -n monitoring
    kubectl delete namespace monitoring
    helm install kube-prometheus prometheus-community/kube-prometheus-stack -n monitoring --create-namespace -f values.yaml
    ```
    
    
---
