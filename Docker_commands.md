1. Скачивание образа докер с Jenkins
$ docker pull jenkins/jenkins

2. Запуск контейнера докер локально
$ docker run -p 8080:8080 -p 50000:50000 jenkins/jenkins:latest

3. Команда, которая показывает пароль админа внутри контейнера
$ docker exec -it <container_id> cat /var/jenkins_home/secrets/initialAdminPassword

4. Старт тома с сохраненными данными:
$ docker run -d -p 8080:8080 -p 50000:50000 -v 9a691919553b7cad4f2231785f2eadaadeb6fa933d7a4f0db2fab603dfead22c:/var/jenkins_home jenkins/jenkins:latest