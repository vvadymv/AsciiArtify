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
У всіх трьох випадках сервіс розгортається за допомогою єдиного [шаблону](./hello-world.yaml)

## 1. minikube

```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && chmod +x minikube
./minikube start
k get all -A ; k apply -f ./hello-world.yaml ; 
k port-forward svc/hello-world-service 8080:80 --pod-running-timeout=10s & 
curl -v localhost:8080
```