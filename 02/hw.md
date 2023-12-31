# Домашнее задание к занятию 2. «Применение принципов IaaC в работе с виртуальными машинами» - Семикова Т.В. FOPS-9

## Задача 1

- Опишите основные преимущества применения на практике IaaC-паттернов.
- Какой из принципов IaaC является основополагающим?

## Ответ
CI паттерн - непрерывная интеграция - набор практик и принципов разработки программного обеспечения, в которой члены команды проводят интеграцию как можно чаще. 
Каждая такая операция должна приводить к ряду автоматических проверок, что позволяет еще на ранних этапах разработки обнаруживать проблемы. 
Непрерывную интеграцию в основном используют в проектах с большим числом разработчиков или несколькими командами разработки, потому что она позволяет снизить трудоемкость процесса 
и сделать его более предсказуемым за счет наиболее раннего обнаружения и устранения ошибок и противоречий.
CD паттерн -непрерывная доставка - позволяет выпускать изменения небольшими партиями, которые легко изменить или устранить путём отката на предыдущую версию и последующего перезапуска процесса сборки с учётом исправления
выявленных дефектов. Подход позволяет уменьшить стоимость, время и риски внесения изменений путём более частных мелких обновлений в продакшн-приложение.
CD паттерн - непрерывное развертывание - практика, позволяющая исключить маскимально ручные действия или их утверждения в процессе развертнывания. Как правило не используется.

Основополагающим является паттерн CI  - без непрерывной интеграции изменений невозможны ни ее дальнейшая доставка, ни развертывание.


## Задача 2

- Чем Ansible выгодно отличается от других систем управление конфигурациями?
- Какой, на ваш взгляд, метод работы систем конфигурации более надёжный — push или pull?

## Ответ
Ansible отличается простотой использования, имеет безагентную архитектуру (не требует установки агента/клиента на целевую систему) и YAML-подобный DSL, написана на Python и легко расширяется за счет модулей. 
Обычно управляет конфигурацией Linux.
Считаю метод push более надежным, потому как результат в таком случае более предсказуем и инициирован непосредственно управляющим процессом лицом.

## Задача 3

Установите на личный компьютер:

- [VirtualBox](https://www.virtualbox.org/),
- [Vagrant](https://github.com/netology-code/devops-materials),
- [Terraform](https://github.com/netology-code/devops-materials/blob/master/README.md)  версии 1.5.Х (1.6.х может вызывать проблемы с яндекс-облаком),
- Ansible.

*Приложите вывод команд установленных версий каждой из программ, оформленный в Markdown.*

## Ответ
```bash
[root@fedora ~]# vboxmanage --version
6.1.48r159471
[root@fedora ~]# vagrant --version
Vagrant 2.2.19
[root@fedora Загрузки]# terraform --version
Terraform v1.5.7
on linux_386
[root@fedora ~]# ansible --version
ansible [core 2.14.11]
  config file = /etc/ansible/ansible.cfg
  configured module search path = ['/root/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3.11/site-packages/ansible
  ansible collection location = /root/.ansible/collections:/usr/share/ansible/collections
  executable location = /usr/bin/ansible
  python version = 3.11.6 (main, Oct  3 2023, 00:00:00) [GCC 12.3.1 20230508 (Red Hat 12.3.1-1)] (/usr/bin/python3)
  jinja version = 3.0.3
  libyaml = True
```

## Задача 4 

Воспроизведите практическую часть лекции самостоятельно.

- Создайте виртуальную машину.
- Зайдите внутрь ВМ, убедитесь, что Docker установлен с помощью команды
```
docker ps,
```
Vagrantfile из лекции и код ansible находятся в [папке](https://github.com/netology-code/virt-homeworks/tree/virt-11/05-virt-02-iaac/src).

Примечание. Если Vagrant выдаёт ошибку:
```
URL: ["https://vagrantcloud.com/bento/ubuntu-20.04"]     
Error: The requested URL returned error: 404:
```

выполните следующие действия:

1. Скачайте с [сайта](https://app.vagrantup.com/bento/boxes/ubuntu-20.04) файл-образ "bento/ubuntu-20.04".
2. Добавьте его в список образов Vagrant: "vagrant box add bento/ubuntu-20.04 <путь к файлу>".

*Приложите скриншоты в качестве решения на эту задачу.*
![ad](https://github.com/SemikovaTV/hw_virtualization/blob/main/02/%D0%92%D1%8B%D0%B4%D0%B5%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5_002.png)

![ad](https://github.com/SemikovaTV/hw_virtualization/blob/main/02/%D0%92%D1%8B%D0%B4%D0%B5%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5_004.png)

![ad](https://github.com/SemikovaTV/hw_virtualization/blob/main/02/%D0%92%D1%8B%D0%B4%D0%B5%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5_005.png)

![ad](https://github.com/SemikovaTV/hw_virtualization/blob/main/02/%D0%92%D1%8B%D0%B4%D0%B5%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5_006.png)




