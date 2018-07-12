# Pody i Deployment
Uruchomienie poda:
```
kubectl run nginx --image=nginx
```
Wyświetlenie składowych poda
```
kubectl get pods -l run=nginx
```
Pobierz dokładną nazwę poda:
```
POD_NAME=$(kubectl get pods -l run=nginx -o jsonpath="{.items[0].metadata.name}")
```
Wykonaj port-forwarding:
```
kubectl port-forward $POD_NAME 8080:80
```
Testujemy:
```
curl --head http://127.0.0.1:8080
```
Logowanie:
```
kubectl logs $POD_NAME
```
Exec:
```
kubectl exec -ti $POD_NAME -- nginx -v
kubectl exec -ti $POD_NAME -- bash
```