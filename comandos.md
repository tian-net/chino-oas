# Despliegue ElChino en EC2

## 1. Clonar el repo
```bash
git clone https://github.com/tian-net/chino-oas.git
cd chino-oas
```

## 2. Aplicar todo
```bash
kubectl apply -f namespace.yaml
kubectl apply -f mongo-deployment.yaml
kubectl apply -f mongo-service.yaml
kubectl apply -f backend-deployment.yaml
kubectl apply -f backend-service.yaml
kubectl apply -f frontend-deployment.yaml
kubectl apply -f frontend-service.yaml
```

## 3. Verificar
```bash
kubectl get all -n elchino
```

## 4. Acceder
```
Frontend: http://IP_PUBLICA_EC2:30080
Backend:  http://IP_PUBLICA_EC2:30001/api/events
```
