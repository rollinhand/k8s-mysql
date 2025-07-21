# MySQL mit phpMyAdmin

Kubernetes Konfiguration mit MySQL und phpMyAdmin.

|Datei|Zweck|
|---|---|
|ConfigMap|enthält nicht-sensible Umgebungsvariablen wie Benutzername oder Hostname
|Secret|enthält sensible Daten wie Passwörter – Rancher zeigt diese sicher an
|PVC|sorgt für persistente Daten für Postgres und PgAdmin
|Deployments|erstellen jeweils einen Pod (postgres, pgadmin), mit Umgebung und Storage
|Services|ermöglichen Kommunikation und externe Erreichbarkeit über Port-Forward oder NodePort

## Installation

```bash
kubectl apply -f k8s/configmap.yaml
kubectl apply -f k8s/secrets.yaml
kubectl apply -f k8s/mysql-pvc.yaml
kubectl apply -f k8s/mysql-deployment.yaml
kubectl apply -f k8s/phpmyadmin-deployment.yaml
kubectl apply -f k8s/services.yaml
```

## Zugriff PgAdmin
Wenn du NodePort nutzt, kannst du mit `kubectl get svc phpmyadmin` die externe Portnummer sehen, z. B.:

```bash
phpmyadmin   NodePort   10.43.52.104   <none>        8081:30090/TCP
```

Dann kannst du aufrufen: http://localhost:30090

**Login in phpMyAdmin:**

|Feld|Wert
|---|---
|Benutzername|root
|Passwort|mySQLr00t