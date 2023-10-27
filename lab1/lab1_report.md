University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FICT](https://fict.itmo.ru)  
Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)  
Year: 2023/2024  
Group: K4111c  
Author: Trieu Minh Tam
Lab: Lab1  
Date of create: 19.10.2023  
Date of finished:  

1. Запускаем minikube. <br>
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/c476cfba-236b-434a-be3b-40ebbbe356b1) <br>

2. Создаём файл деплоймента. <br>
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: vault
  labels:
    owner: trieu
spec:
  replicas: 2
  selector:
    matchLabels:
      app: vault
  template:
    metadata:
      labels:
        app: vault
    spec:
      containers:
      - name: vault
        image: vault:1.13.3
        ports:
        - containerPort: 8200
```

