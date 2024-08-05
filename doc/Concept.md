1. minikube
1. kind 
1. k3d

Вступ: Опис інструментів та їх призначення.
Характеристики: Опис основних характеристик кожного інструменту, таких як підтримувані ОС та архітектури, можливість автоматизації, наявність додаткових функцій, таких як моніторинг та керування Kubernetes кластером.
Переваги та недоліки: Опис переваг та недоліків кожного інструменту, таких як легкість використання, швидкість розгортання, стабільність роботи, наявність документації та підтримки спільноти, складність налаштування та використання.
Демонстрація: Коротка демонстрація рекомендованого Вами інструменту з використанням прикладу, такого як розгортання застосунку «Hello World» на Kubernetes.
Висновки: Заключення та рекомендації щодо використання кожного інструменту в PoC для стартапу.

# Include asciinema recording
![Image](.data/demo.gif)


# Table example
| Skills                              | Junior SRE Tools/Technologies                                     | Middle SRE Tools/Technologies                                       | Senior SRE Tools/Technologies                                                        | Principal SRE Tools/Technologies                                                  |
|-------------------------------------|-------------------------------------------------------------------|---------------------------------------------------------------------|--------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|
| Infrastructure and Networking       | Linux, Bash, TCP/IP, DNS, Load Balancers                          | Advanced networking tools like F5, Citrix, Cloudflare, etc.         | Advanced networking tools like Cisco, Juniper, and Arista                            | Design custom hardware and software networking solutions                          |


# Кроки для відтворення тесту.
У всіх трьох випадках сервіс розгортається за допомогою єдиного [шаблону](../hello-world.yaml)

## 1. minikube
### 1.1 Deploy:
```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && chmod +x minikube && ./minikube start 
```
### 1.2 Тестовий сервіс:
```
k get all -A && k apply -f ./doc/hello-world.yaml && k get all
k port-forward svc/hello-world-service 8081:8080 & 
```
### 1.3 Перевірка:
```
curl -v localhost:8081
curl localhost:8081
kubectl logs `kubectl get pods --output=name`
```
```
./minikube delete
```

## 2. kind 
### 2.1 Deploy:
```
[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.23.0/kind-linux-amd64 && chmod +x kind && ./kind create cluster --name kind-cluster
```

### 2.2 Тестовий сервіс:
```
k get all -A && k apply -f ./hello-world.yaml && k port-forward svc/hello-world-service 8080:8080 --pod-running-timeout=10s & 
```
### 2.3 Перевірка:
```
curl -v localhost:8080
```


## 3. k3d 
### 3.1 Deploy:
```
curl -s https://raw.githubusercontent.com/rancher/k3d/main/install.sh | bash && k3d cluster create k3d-cluster 
```

### 3.2 Тестовий сервіс:
```
k get all -A && k apply -f ./hello-world.yaml && k port-forward svc/hello-world-service 8080:80 --pod-running-timeout=10s & 
```
### 3.3 Перевірка:
```
curl -v localhost:8080
```

