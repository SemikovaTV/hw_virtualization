
# Домашнее задание к занятию 1.  «Введение в виртуализацию. Типы и функции гипервизоров. Обзор рынка вендоров и областей применения» - Семикова Т.В. FOPS-9

## Задача 1

Опишите кратко, в чём основное отличие полной (аппаратной) виртуализации, паравиртуализации и виртуализации на основе ОС.

## Ответ:
Аппаратная виртуализация - позволяет создавать независимые и изолированные друг от друга виртуальные компьютеры с помощью программной имитации ресурсов (процессора, памяти, сети, диска и др.) физического сервера. Физический сервер называют хостовой машиной, виртуальные компьютеры – виртуальными машинами. Программное обеспечение, которое создает виртуальные машины и управляет ими, называют гипервизором. На практике на виртуальных машинах могут использоваться разные ОС для разных целей.

Паравиртуализация - разновидность виртуализации, при которой гостевая операционная система модифицируется перед установкой внутри виртуальной машины, чтобы позволить всем гостевым ОС в системе совместно использовать ресурсы. Операционная система взаимодействует с программой гипервизора, который предоставляет ей гостевой API, вместо использования напрямую таких ресурсов, как таблица страниц памяти.
Метод паравиртуализации применим лишь в том случае, если гостевые операционные системы имеют открытые исходные коды, которые можно модифицировать согласно лицензии, или же гипервизор и гостевая операционная система разработаны одним производителем с учётом возможности паравиртуализации гостевой системы.
Основное различие между паравиртуализацией и аппаратной виртуализацией заключается в возможности внесения изменений в гостевую ОС. При паравиртуализации гостевая ОС знает, что она виртуализируется. При аппаратной виртуализации немодифицированная ОС работает так же, как если бы она не была виртуализирована.

Виртуализация на основе ОС (контейнеризация) -Это виртуализация на уровне операционной системы. Если аппаратная виртуализация полностью эмулирует оборудование и позволяет запускать любые ОС, внутри контейнера можно запустить только аналогичную хосту операционную систему. Преимуществом этого подхода является скорость, с которой создаётся контейнер — секунды, тогда как для запуска виртуальной машины счёт времени идёт на минуты. Так происходит потому, что полноценной виртуальной машине нужно сначала инициализировать всё оборудование, запустить эмуляцию и только после этого начать загружать операционную систему. При контейнеризации ОС по факту уже работает. Остаётся только создать замкнутую среду — тот самый контейнер, в котором будет запущен ещё один экземпляр операционной системы.
Контейнер представляет собой всего лишь один процесс, внутри которого выполняется операционная система. Она существует в своём собственном мире, со своей сетью, своим диском, своей файловой системой и так далее. Эту виртуализацию применяют на уровне сервисов, составляющих части программного продукта. 

## Задача 2

Выберите один из вариантов использования организации физических серверов в зависимости от условий использования.

Организация серверов:

- физические сервера,
- паравиртуализация,
- виртуализация уровня ОС.

Условия использования:

- высоконагруженная база данных, чувствительная к отказу;
- различные web-приложения;
- Windows-системы для использования бухгалтерским отделом;
- системы, выполняющие высокопроизводительные расчёты на GPU.

Опишите, почему вы выбрали к каждому целевому использованию такую организацию.

## Ответ:
- высоконагруженная база данных, чувствительная к отказу - виртуализация уровня ОС с внешним хранилищем данных и репликацией.
- различные web-приложения - виртуализация уровня ОС
- Windows-системы для использования бухгалтерским отделом - физические сервера, обязательно бекап.
- системы, выполняющие высокопроизводительные расчёты на GPU - паравиртуализация, поскольку позволяет добиться более высокой производительности. 

## Задача 3

Выберите подходящую систему управления виртуализацией для предложенного сценария. Детально опишите ваш выбор.

Сценарии:

1. 100 виртуальных машин на базе Linux и Windows, общие задачи, нет особых требований. Преимущественно Windows based-инфраструктура, требуется реализация программных балансировщиков нагрузки, репликации данных и автоматизированного механизма создания резервных копий.
2. Требуется наиболее производительное бесплатное open source-решение для виртуализации небольшой (20-30 серверов) инфраструктуры на базе Linux и Windows виртуальных машин.
3. Необходимо бесплатное, максимально совместимое и производительное решение для виртуализации Windows-инфраструктуры.
4. Необходимо рабочее окружение для тестирования программного продукта на нескольких дистрибутивах Linux.

## Ответ:
1. 100 виртуальных машин на базе Linux и Windows, общие задачи, нет особых требований. Преимущественно Windows based-инфраструктура, требуется реализация программных балансировщиков нагрузки, репликации данных и автоматизированного механизма создания резервных копий.
Hyper-V -  поскольку преимущественно Windows based-инфраструктура, репликация возможна встроенными средствами гипервизора, встроенная балансировка нагрузки с возможностью ручной настройки.
2. Требуется наиболее производительное бесплатное open source-решение для виртуализации небольшой (20-30 серверов) инфраструктуры на базе Linux и Windows виртуальных машин.
KVM - поскольку без особых сложностей работает со средой Windows и является open source решением.
4. Необходимо бесплатное, максимально совместимое и производительное решение для виртуализации Windows-инфраструктуры.
5. KVM - поскольку без особых сложностей работает со средой Windows и является open source решением.
6. Необходимо рабочее окружение для тестирования программного продукта на нескольких дистрибутивах Linux.
LXC  - Linux контейнеры - позволяет развернуть несколько полностью изолированных экземпляров ОС Linux на одном компьютере/сервере, создать кластер, позволяет гибко менять размер диска, расширять RAM, добавлять ядра процессора без перезагрузки, создавать внутреннюю сеть между контейнерами.


## Задача 4

Опишите возможные проблемы и недостатки гетерогенной среды виртуализации (использования нескольких систем управления виртуализацией одновременно) и что необходимо сделать для минимизации этих рисков и проблем. Если бы у вас был выбор, создавали бы вы гетерогенную среду или нет? Мотивируйте ваш ответ примерами.

## Ответ:
К недостаткам можно отнести:
- сложность управления и администрирования из-за использования различных технологий под реализацию задач;
- сложность перемещения данных из физической среды в виртуальную и наоборот;
- наличие высококовалифицированных специалистов;
- стоимость обслуживания.

Для реализации гетерогенной среды и минимизации рисков нужно:
- использовать комплексные решения, подходящие и для физической и для виртуальной среды;
- макимально снизить вероятность несовместимости технологий и упростить управление инфраструктурой;
- универсальная платформа для перемещения и защиты данных;
- обязательно бекап.

В качестве опыта - думаю да, поскольку у гомогенной среды есть существенный недостаток - сложность отказа, поскольку появляется зависимость от одного конкретного вендора и его сервисов, в то время как гетерогенная среда дает больше возможностей для гибкого изменения архитектуры в будущем.

