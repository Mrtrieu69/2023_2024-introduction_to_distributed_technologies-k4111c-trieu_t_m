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
minikube start --network-plugin=cni --cni=calico --nodes 2 --driver=virtualbox --no-vtx-check 
```
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/1fc95693-65e9-43c2-8871-36973cb173f6)<br>
Список нодов<br>
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/01b7fc61-e63f-4a6e-9b78-b4c98e8207d2)<br>
Calico установлен<br>
![image](https://github.com/Mrtrieu69/2023_2024-introduction_to_distributed_technologies-k4111c-trieu_t_m/assets/87965299/582c509c-db9a-4c95-acdc-46896ed20af7)<br>
2. 
