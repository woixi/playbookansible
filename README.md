мини инструкция 
1. Переходим в директорию docker где лежат докерфайлы 
2. билдим контейнеры и запускаем
```
docker-compose build
docker-compose up -d 
```
3. Переходим в директорию ansible 
4. Запускаем плейбук
```
ansible-playbook -i inventory.ini playbook.yml
```
по завершению на 
http://localhost:8080/images/ 
или
http://localhost:80/images/
будет список доступных статик файлов

(у меня просто 80 порт занят и редиректит на 8080) 
