# Домашнее задание к занятию "`Что такое DevOps? CI/CD`" - `Егоркин Александр`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1



1. Установите себе jenkins по инструкции из лекции или любым другим способом из официальной документации. Использовать Docker в этом задании нежелательно.
   [Jenkins installed](https://github.com/sash39/DevOps_CI-CD/assets/11473102/32113ae5-3739-4ae8-ac94-45403c6e86c3)
3. Установите на машину с jenkins golang.[Golang installed](https://github.com/sash39/DevOps_CI-CD/assets/11473102/2cad7ba3-6255-49ca-b26e-7d61b557e8dc)
4. Создайте в jenkins Freestyle Project, подключите получившийся репозиторий к нему и произведите запуск тестов и сборку проекта go test . и docker build .. (https://github.com/sash39/DevOps_CI-CD/assets/11473102/3ceec8c8-4b4d-44d2-9c7d-9a91c5a41693)
  (https://github.com/sash39/DevOps_CI-CD/assets/11473102/bc527789-75c1-4348-91e2-5f8bfbdc601d)  (https://github.com/sash39/DevOps_CI-CD/assets/11473102/1afa206e-60c7-4a6b-a757-284301bbc53c)


### Задание 2


1. Создайте новый проект pipeline.
2. Перепишите сборку из задания 1 на declarative в виде кода.
В качестве ответа пришлите скриншоты с настройками проекта и результатами выполнения сборки.

Скриншоты
[Succeed](https://github.com/sash39/DevOps_CI-CD/assets/11473102/f597beb6-b43f-4baa-8ea8-defe10e1fc8d),
[Configure](https://github.com/sash39/DevOps_CI-CD/assets/11473102/e7da5afb-edd6-4ef2-923f-90bd74a49de3)


### Задание 3

1. Установите на машину Nexus. https://vaiti.io/ustanavlivaem-i-nastraivaem-sonatype-nexus-repository-dlya-raboty-s-repozitoriyami-docker/
[nexus](https://github.com/sash39/DevOps_CI-CD/assets/11473102/7341336d-d27e-43e5-9bc1-2db7282a2328)
   
3. Создайте raw-hosted репозиторий.
   [raw-hosted](https://github.com/sash39/DevOps_CI-CD/assets/11473102/f56203c4-b6ad-444a-aa7a-75e152725c78)
   
5. Измените pipeline так, чтобы вместо Docker-образа собирался бинарный go-файл. Команду можно скопировать из Dockerfile.
[pipeline](https://github.com/sash39/DevOps_CI-CD/assets/11473102/ec3bc40b-7ff8-4d62-b014-eac2d42dd4ad)
[pipeline2](https://github.com/sash39/DevOps_CI-CD/assets/11473102/083f44c3-005b-45b2-b1e6-1e36f308a451)
7. 
Загрузите файл в репозиторий с помощью jenkins.
[go](https://github.com/sash39/DevOps_CI-CD/assets/11473102/7d7a0128-80eb-4a69-9c27-8203488beadc)


### Задание 4


Придумайте способ версионировать приложение, чтобы каждый следующий запуск сборки присваивал имени файла новую версию. Таким образом, в репозитории Nexus будет храниться история релизов.

Подсказка: используйте переменную BUILD_NUMBER.

В качестве ответа пришлите скриншоты с настройками проекта и результатами выполнения сборки.
(https://github.com/sash39/DevOps_CI-CD/assets/11473102/343ef601-0d99-470d-af75-d50000e722e5)

ФАЙЛЫ в NEXUS
[files](https://github.com/sash39/DevOps_CI-CD/assets/11473102/d8a063ca-56b8-41cc-af93-59b00107d7d5)


```
pipeline {
    agent any

    environment {
        NEXUS_REPO_URL = 'http://127.0.0.1:8081/repository/raw/'
    }

    stages {
        stage('Git') {
            steps {
                git 'https://github.com/netology-code/sdvps-materials.git'
            }
        }

        stage('Build Go App') {
            steps {
                script {
                    // Сборка Go-приложения с динамическим именем файла
                    sh "CGO_ENABLED=0 GOOS=linux go build -a -installsuffix nocgo -o myapp-v${BUILD_NUMBER}"
                }
            }
        }

        stage('Upload to Nexus') {
            steps {
                script {
                    // Загрузка бинарного файла в Nexus с динамическим именем файла
                    sh "curl -v -u admin:admin --upload-file myapp-v${BUILD_NUMBER} ${NEXUS_REPO_URL}myapp-v${BUILD_NUMBER}"
                }
            }
        }
    }
}

```


