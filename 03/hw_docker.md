# Домашнее задание к занятию 3. «Введение. Экосистема. Архитектура. Жизненный цикл Docker-контейнера» - Семикова Т.В. FOPS-9

## Задача 1

Сценарий выполнения задачи:

- создайте свой репозиторий на https://hub.docker.com;
- выберите любой образ, который содержит веб-сервер Nginx;
- создайте свой fork образа;
- реализуйте функциональность:
запуск веб-сервера в фоне с индекс-страницей, содержащей HTML-код ниже:
```
<html>
<head>
Hey, Netology
</head>
<body>
<h1>I’m DevOps Engineer!</h1>
</body>
</html>
```
Опубликуйте созданный fork в своём репозитории и предоставьте ответ в виде ссылки на https://hub.docker.com/username_repo.

## Ответ
Мне не удалось зарегистрироваться на https://hub.docker.com, покажу тут поэтапно:

1. Скачиваем образ nginx:
```bash
docker pull nginx
```
2. Создаем Dockerfile:
```bash
FROM nginx
RUN echo '<html><head>Hey, Netology</head><body><h1>I am DevOps Engineer!</h1></body></html>' > /usr/share/nginx/html/index.html
```
![ad](https://github.com/SemikovaTV/hw_virtualization/blob/main/03/%D0%92%D1%8B%D0%B4%D0%B5%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5_010.png)
3.Собираем образ:
```bash
docker build -t semikova/nginx:1 .
```
![ad](https://github.com/SemikovaTV/hw_virtualization/blob/main/03/%D0%92%D1%8B%D0%B4%D0%B5%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5_009.png)
4. Смотрим наши образы:
![ad](https://github.com/SemikovaTV/hw_virtualization/blob/main/03/%D0%92%D1%8B%D0%B4%D0%B5%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5_008.png)
5. Запускаем контейнер:
```bash
docker run -d -p 8080:80 semikova/nginx:1
```
6. Проверяем:
![ad](https://github.com/SemikovaTV/hw_virtualization/blob/main/03/%D0%92%D1%8B%D0%B4%D0%B5%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5_007.png)

## Задача 2

Посмотрите на сценарий ниже и ответьте на вопрос:
«Подходит ли в этом сценарии использование Docker-контейнеров или лучше подойдёт виртуальная машина, физическая машина? Может быть, возможны разные варианты?»

Детально опишите и обоснуйте свой выбор.

--
## Ответ:

Сценарий:

- высоконагруженное монолитное Java веб-приложение - физическая машина;
- Nodejs веб-приложение - Docker;
- мобильное приложение c версиями для Android и iOS - Docker;
- шина данных на базе Apache Kafka - Docker;
- Elasticsearch-кластер для реализации логирования продуктивного веб-приложения — три ноды elasticsearch, два logstash и две ноды kibana - Docker;
- мониторинг-стек на базе Prometheus и Grafana - Docker;
- MongoDB как основное хранилище данных для Java-приложения - физическая машина;
- Gitlab-сервер для реализации CI/CD-процессов и приватный (закрытый) Docker Registry - виртуальная машина или Docker;

## Задача 3

- Запустите первый контейнер из образа ***centos*** c любым тегом в фоновом режиме, подключив папку ```/data``` из текущей рабочей директории на хостовой машине в ```/data``` контейнера.
- Запустите второй контейнер из образа ***debian*** в фоновом режиме, подключив папку ```/data``` из текущей рабочей директории на хостовой машине в ```/data``` контейнера.
- Подключитесь к первому контейнеру с помощью ```docker exec``` и создайте текстовый файл любого содержания в ```/data```.
- Добавьте ещё один файл в папку ```/data``` на хостовой машине.
- Подключитесь во второй контейнер и отобразите листинг и содержание файлов в ```/data``` контейнера.

## Ответ
1. Создаем контейнер centos:
```bash
docker run -v /data:/data --name centos_container -t -d centos /bin/bash
```
2. Создаем контейнер debian:
```bash
docker run -v /data:/data --name debian_container -t -d debian /bin/bash
```
3. Смотрим список контейнеров: 
```bash
[root@fedora containers_hw]# docker container ps
CONTAINER ID   IMAGE              COMMAND                  CREATED              STATUS                  NAMES
5f12021e423b   debian             "/bin/bash"              About a minute ago   Up About a minute       debian_container
7996871014db   centos             "/bin/bash"              11 minutes ago       Up 11 minutes           centos_container
```
4. Подключаемся к centos_container и создаем файл:
```bash
[root@fedora containers_hw]# docker exec -it centos_container /bin/bash
[root@7996871014db /]# cd /data
[root@7996871014db data]# touch test_file_1.txt
```
5. Возвращаемся на хостовую машину и создаем файл:
```bash
[root@fedora containers_hw]# cd /data/
[root@fedora data]# touch test_file_2.txt
```
6. Подкючаемся к debian_container и смотрим содержимое /data:
```bash
[root@fedora data]# docker exec -it debian_container /bin/bash
root@5f12021e423b:/# cd /data/
root@5f12021e423b:/data# ls
test_file_1.txt  test_file_2.txt
```
