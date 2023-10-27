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
3. Разворачиваем его в кластере.<br>
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/1f2937df-2b6c-41bc-bd93-3a9d2faebc26)<br>
4. Деплоим сервис. <br>
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/13fa3b4c-2927-4f16-9608-facd3bf1de1f)
5. В discribe выводим адрес для доступа к приложения <br>
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/179ccdcd-6456-44d3-a81e-1d1d2fe183c2)
6. Прокидываем порт и волт открывается в браузере.
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/6da87e82-1400-44cf-a28d-baa62f1c7204)
7. Для получения токена открываем логи пода, используем команду<br>
```
 kubectl logs [name-pod]
```
8. Учетные данные находятся в конце вывода. <br>
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/4bfc46a3-bb59-466b-a3a9-d49b35358dc7)
9. Используем учетные данные для аутентификации, после чего мы попадем на эту страницу.<br>
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/1ea4c6fd-20ab-457c-a1c7-1e79b630482b)
10. После чего, останавливаем minikube <br>
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/0fc0781d-ea1a-4844-a423-a4c82ced521e)
