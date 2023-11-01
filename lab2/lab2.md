University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FICT](https://fict.itmo.ru)  
Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)  
Year: 2023/2024  
Group: K4111c  
Author: Trieu Minh Tam
Lab: Lab2  
Date of create: 29.10.2023  
Date of finished:

1. Запускаем minikube. <br>
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/b5a976fa-dbc1-44b7-89df-2bab06d0e0aa)<br>
2. Создаём файл деплоймента и запускаем файл. <br>
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app
  labels:
    app: app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: app
  template:
    metadata:
      labels:
        app: app
    spec:
      containers:
      - name: app
        image: ifilyaninitmo/itdt-contained-frontend:master
        env:
        - name: REACT_APP_USERNAME
          value: "trieutam"
        - name: REACT_APP_COMPANY_NAME
          value: "krayt"
        ports:
        - containerPort: 3000
```
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/c07a025b-09db-4116-a45d-1db733a51b8e)<br>
3. Создаём сервис, чтобы сделать наше развертывание доступным для внешнего трафика.<br>
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/efda899d-77dc-4618-aa32-4f6e660bc3ef)<br>
4. Запускаем режим переадресации портов для доступа к нашим контейнерам через браузер. <br>
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/2d881297-22c8-4858-93d3-73d32f93b434)<br>
5. Наше приложение в веб-браузере<br>
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/e180498f-b8cf-4566-9cfd-bbbe7181ae10)<br>
соответствуют тем, которые были переданы в коде. Также указано название пода и айпи - оно может меняться в завимости от того, в какой под идёт запрос. У нас две реплики, в браузере отображается информация одной из них.<br>
6. Логи контейнеров<br>
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/1a9c57d1-4cc0-432f-9b6a-8a5f20268e63)<br>
7. Схема<br>
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/e014e854-69d1-442f-8314-9bfcf9c69e23)


