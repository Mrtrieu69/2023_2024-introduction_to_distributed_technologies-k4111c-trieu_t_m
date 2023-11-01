University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FICT](https://fict.itmo.ru)  
Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)  
Year: 2023/2024  
Group: K4111c  
Author: Trieu Minh Tam<br>
Lab: Lab3  
Date of create: 01.11.2023  
Date of finished:

1. Создаём ConfigMap со значениями переменных. <br>
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: values
  namespace: secretapp
data:
  react_app_username: "trieutam"
  react_app_company_name: "krayt"
```
2. Создаём ReplicaSet, в который передаём указанные переменные. <br>
```
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: secretapp
  namespace: secretapp
spec:
  replicas: 2
  selector:
    matchLabels:
      tier: secretapp
  template:
    metadata:
      labels:
        tier: secretapp
    spec:
      containers:
      - name: secretapp
        image: ifilyaninitmo/itdt-contained-frontend:master
        env:
        - name: REACT_APP_USERNAME
          valueFrom:
            configMapKeyRef:
              name: values
              key: react_app_username
        - name: REACT_APP_COMPANY_NAME
          valueFrom:
            configMapKeyRef:
              name: values
              key: react_app_company_name

```
3. Запускаем файл yaml для создания replicaset<br>
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/9283a8a8-1e4c-43a0-8170-b1610698c593)<br>
4. Включаем ingress. <br>
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/001e0ecb-2bdf-4b79-bbce-19dce31514ee)



