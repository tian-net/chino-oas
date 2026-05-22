# Despliegue ElChino en EC2

## 1. Clonar el repo
```bash
git clone https://github.com/tian-net/chino-oas.git
cd chino-oas
```

## 2. Construir imágenes Docker (opcional, ya están en Docker Hub)
```bash
# Backend
docker build -t tian11qb/sebastian-webflux-nosql:lastest -f backend/Dockerfile .

# Frontend
docker build -t tian11qb/sebastian-front-react-vite-tailwind:lastest -f frontend/Dockerfile .
```

## 3. Aplicar todo
```bash
kubectl apply -f namespace.yaml
kubectl apply -f mongo-deployment.yaml
kubectl apply -f mongo-service.yaml
kubectl apply -f backend/deployment.yaml
kubectl apply -f backend/service.yaml
kubectl apply -f frontend/deployment.yaml
kubectl apply -f frontend/service.yaml
```

## 4. Verificar
```bash
kubectl get all -n elchino
# Esperar hasta que todos los pods estén en "Running"
```

## 5. Exponer servicios (Minikube)
```bash
kubectl port-forward -n elchino service/frontend-service 30080:80 --address 0.0.0.0 &
kubectl port-forward -n elchino service/backend-service 30001:30001 --address 0.0.0.0 &
```

## 6. Acceder
```
Frontend:  http://IP_PUBLICA_EC2:30080
Backend:   http://IP_PUBLICA_EC2:30001/api/events
Swagger:   http://IP_PUBLICA_EC2:30001/swagger-ui.html
```

## Expandir volumen EBS (si hay errores de espacio)
```bash
sudo growpart /dev/nvme0n1 1
sudo resize2fs /dev/nvme0n1p1
df -h
```
