# WordPress + MySQL on Kubernetes (with Deployment, Service, PVC, PV)

This project provides a basic setup to deploy **WordPress** and **MySQL** using Kubernetes with:

- Deployment (for WordPress and MySQL)
- PersistentVolume (PV)
- PersistentVolumeClaim (PVC)
- Services for internal and external access
- Namespace: `wordpress-app`

## 📁 Project Structure

```
k8s-wordpress-yaml/
├── namespace.yaml
├── mysql/
│   ├── mysql-deployment.yaml
│   ├── mysql-service.yaml
│   ├── mysql-pv.yaml
│   └── mysql-pvc.yaml
├── wordpress/
│   ├── wordpress-deployment.yaml
│   ├── wordpress-service.yaml
│   ├── wordpress-pv.yaml
│   └── wordpress-pvc.yaml
└── README.md
```

## 🚀 Deployment Steps

1. **Clone the repo** (if already uploaded to GitHub):
   ```bash
   git clone https://github.com/yourusername/k8s-wordpress-yaml.git
   cd k8s-wordpress-yaml
   ```

2. **Apply the namespace**:
   ```bash
   kubectl apply -f namespace.yaml
   ```

3. **Apply MySQL configs**:
   ```bash
   kubectl apply -f mysql/ -n wordpress-app
   ```

4. **Apply WordPress configs**:
   ```bash
   kubectl apply -f wordpress/ -n wordpress-app
   ```

5. **Check deployments**:
   ```bash
   kubectl get all -n wordpress-app
   ```

6. **Access WordPress**:
   - If using NodePort: `http://<node-ip>:<nodeport>`
   - If using Ingress: adjust service accordingly.

## 💾 Persistent Storage

- **MySQL PVC** → Bound to `mysql-pv` (local or NFS volume)
- **WordPress PVC** → Bound to `wordpress-pv`

## ⚙️ Customization

- Modify `mysql-deployment.yaml` to change `MYSQL_ROOT_PASSWORD` or DB name.
- Modify `wordpress-deployment.yaml` to point to custom DB host or credentials.
- Update PVC sizes, storage class, or access modes in PVC/YAML files.

## 🧹 Cleanup

To remove all resources:
```bash
kubectl delete -f . -R -n wordpress-app
kubectl delete namespace wordpress-app
```

---

Created with ❤️ for learning and deployment of WordPress on Kubernetes.
