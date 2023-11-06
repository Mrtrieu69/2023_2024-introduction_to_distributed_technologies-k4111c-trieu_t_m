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
