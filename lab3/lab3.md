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
4. Запускаем сервер<br>
```
kubectl expose deployment web-deployment --type=NodePort --port=3000 -n reactapp -n secretapp
```
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/04112a37-3938-407a-9184-892aef0e01b0)<br>
5. Получаем доступ к контайнеру через port 31442<br>
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/8cb1e78c-3ecf-4e43-925f-a034b80ee555)<br>
6. Включаем ingress. <br>
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/001e0ecb-2bdf-4b79-bbce-19dce31514ee)<br>
7. Создаем сертификат <br>
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/658a214d-d4e8-4eaa-b403-641e78d353ce)<br>
8. Импортируем сертификат в наш кластер.<br>
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/5d95145e-826a-4720-af61-13a5a7a4485e)
9. Создаем файл ingress.yaml, затем запускаем его. <br>
```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: secretapp
  namespace: secretapp
spec:
  tls:
  - hosts:
      - secretapp.info
    secretName: secret-tls
  rules:
  - host: secretapp.info
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: secretapp
            port:
              number: 3000
```
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/e82840b4-447e-4af2-902e-3814011acca0)<br>
10. Отредактируем файл хостов, включив в него имя нашего хоста secretapp.info. <br>
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/47da0c8c-8a4c-4222-84e9-dff2ecad65c9)<br>
11. Получаем доступ к приложению через браузер, используя имя хоста edu.info. <br>
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/cc76d679-347c-4245-82e0-7b7dd0fc7257)<br>
12. Наш сертификат.<br>
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/004b2534-e28c-4ca6-b774-951c7a0468ae)<br>
13. Схема<br>
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/cbc78239-0d35-4d26-abfd-0d622cd9b6e9)






