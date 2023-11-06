University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FICT](https://fict.itmo.ru)  
Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)  
Year: 2023/2024  
Group: K4111c  
Author: Trieu Minh Tam<br>
Lab: Lab4  
Date of create: 06.11.2023  
Date of finished:

1. Запускаем миникуб с подключенным плагином калико и двумя нодами. <br>
```
minikube start --network-plugin=cni --cni=calico --nodes 2 --driver=docker --no-vtx-check
```
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/38c8eb2c-3b4d-42bc-8438-4077eadec78f)<br>
Список нодов и Calico установлен<br>
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/6df865b0-fdcb-4089-970f-be4189ccc33b)<br>
2. Ставим нодам лейблы.<br>
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/43d683dd-d66d-4348-bcf8-92b729e44f80)<br>
3. Создаем файл манифеста для назначения пула IP узлам на основе их меток.<br>
```
apiVersion: projectcalico.org/v3
kind: IPPool
metadata:
  name: master-ippool
spec:
  cidr: 192.168.0.0/24
  ipipMode: Always
  natOutgoing: true
  nodeSelector: name == "master"
---
apiVersion: projectcalico.org/v3
kind: IPPool
metadata:
  name: worker-ippool
spec:
  cidr: 192.168.1.0/24
  ipipMode: Always
  natOutgoing: true
  nodeSelector: name == "worker"
```
Выполнив файл выше, получаем наши ippool.<br> 
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/39c03a4e-388d-4b22-bbd1-609723dd4285)
4. Создаем файл для деплоя приложения и запускаем его. <br>
```
apiVersion: v1
kind: Namespace
metadata:
  name: app
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app
  namespace: app
spec:
  selector:
    matchLabels:
      app: app
  replicas: 2 
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
          value: "trieutam "
        - name: REACT_APP_COMPANY_NAME
          value: "krayt"
        ports:
        - containerPort: 3000
```
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/699d734b-3e93-4c90-a442-2422285b3d77)<br>
5. Создаем сервис для получения доступа к сайту.<br> 
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/5b3e8912-185f-404e-938e-ddd3385a8c61)<br>
6. Заходим на под master и пингуем на второй под.<br>
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/4204298f-f4ab-410a-9fd5-ae4369790e26)
7. Схема
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/f83317ff-b945-40cd-b447-4d477d030380)



