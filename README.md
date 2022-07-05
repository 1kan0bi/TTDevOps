# TTDevOps

Данный репозиторий является тестовым заданием на позицию DevOps-инженер.  

## Предисловие к заданию

В репозитории расположено простое скриптовое приложение на языке программирования *(далее по тексту, ЯП)* PHP, с использованием фреймворка [Laravel](https://laravel.com/) сл. версий: 

* Laravel v9.17.0 (PHP v8.1.7)

Контейнерная инфраструктура - является основой всех наших приложений, поэтому для организации полноценного CI/CD-процесса, мы упаковываем все в контейнеры, с использованием программного обеспечения для автоматизации развёртывания и управления приложениями в средах с поддержкой контейнеризации. Таким средством выступает - [Docker](https://docker.com).

На основе подготовленного контейнера, мы пишем конфигурационные файлы для оркестрации и управления группами сервисов, чтобы в последствии запускать наши приложения в development-/production-средах и обеспечивать бесперебойную работу наших решений. 

Прежде чем приступить к выполнению задания, нужно: 

1. Сделать Fork данного проекта в GitHub, 
2. Выполнять задание в fork данного проекта, 
3. По завершению одного или двух блоков задания, оформить Pull Request *(далее по тексту, PR)*, 
4. Ожидать проверки и результатов. 

## Задание

Тестовое задание состоит из нескольких блоков: 

* минимально необходимый, 
* и дополнительный, 

но имеет линейный алгоритм реализации. 

### Цель задания

#### Общая

Определение заявленных теоретических знаний и их практическое применение в работе над заданием. 

#### Конкретная

* Умение писать основные конфигурационные файлы для сборки образов на базе Docker, 
* Наличие понимания того, как работает контейнерная инфраструктура и взаимодействует между собой, 
* Умение работать с информацией из интернета: находить, верно интрепретировать и применять в работе с успешным результатом,
* Умение работать с системами контроля версий: знание основных команд, принципов и их применение в работе, 
* Стиль работы с синтаксисом, знание и соблюдение общих правил написания конфигурационных файлов в соответствии с лучшими практиками. 

### Минимальный необходимый блок 

Для успешного прохождения минимального блока, необходимо: 

  - [x] Написать и добавить **.dockerignore** файл в репозиторий,
  - [x] Написать **Dockerfile** и добавить его в репозиторий для контейнеризации данного приложения, 
  - [x] Провести сборку образа на локальной станции и проверить на наличие ошибок, 
  - [x] Запустить собранный образ и убедиться в успешном результате запуска контейнера в соответствии с ожиданиями ниже, 
  - [x] Написать документацию и добавить ее в репозиторий, с описанием основных команд для сборки образа и запуску контейнера на базе данного образа.

#### Уточнения 

1. Берем за правило, что конечный пользователь - умеет работать с терминалом и знает основные команды Docker,  
2. Docker у пользователя - **установлен**, 
3. Предпочтительный синтаксис разметки документации - Markdown,
4. Данное приложение должно запускаться в контейнере при помощи команды:    
  `#> php artisan serve --host=0.0.0.0`
5. В документации, должны быть описаны все ключи, необходимые для запуска сервиса на базе образа с приложением.  

#### Ожидаемый результат 

По завершению работы над первым блоком, уже можно оформлять PR в основной репозиторий проекта, так как вторая часть является дополнительной и решается по желанию. 

В качестве **результата** проделанной работы, ожидается: 

1. В [основной репозиторий проекта](https://github.com/cardinalit/TTDevOps), оформлен PR,
2. Fork репозиторий содержит все необходимые файлы из задания, 
3. Пользователь может скачать Fork репозиторий для тестирования результатов, 
4. Выполняя последовательно указания из документации по сборке образа и запуску сервиса, пользователь открывает браузер, и перейдя по адресу `http://localhost:8000`, видит загрузку приветственного окна, как представлено ниже на скриншоте: 

![Успешный результат минимального блока с заданием](https://fs.dragops.team/s/rzMZCN9FkmXsgzn/preview)

> **Чтобы увидеть область под блюром, надо выполнить задание! 😉**

### Дополнительный блок 

Второй блок задания делается по желанию, либо по конкретному указанию на то, что он ожидается в исполнении в том числе. 

В работе на production-среде **не используется** конструкция запуска приложения вида `php artisan serve`, как изначально требуется в первом блоке. Тут все сложнее: используется связка web-server *(NGINX в нашем случае)* + php-fpm.

Так как php-fpm работает по потоколу FastCGI, то перед ним должен стоять веб-сервер, который будет проксировать запросы от клиента до самого приложения по схеме `HTTP (1) <--> HTTP (2) <--> FastCGI (3)`, где: 

1. Браузер клиента,
2. Web-server, 
3. php-fpm *(наше приложение)*.

Для успешного прохождения дополнительного блока, необходимо: 

  - [x] Успешно выполнить минимальный блок, 
  - [x] Переписать **Dockerfile** на использование образа `php-fpm` *(версии не ниже v8.1.7)*
  - [x] Подготовить конфигурационный файл Vhost и добавить его в репозиторий для веб-сервера NGINX, который будет заниматься проксированием запросов до нашего сервиса с приложением по протоколу FastCGI,
  - [x] Написать `docker-compose.yml` и добавить его в репозиторий, где будет объявлено два сервиса: веб-сервер и сервис с нашим приложением на базе ранее собранного нами образа c php-fpm, 
  - [x] Провести самостоятельную проверку работоспособности данного решения на локальной машине в соответствии с ожиданиями ниже, 
  - [x] Дополнить ранее созданную документацию, добавив туда инструкцию по запуску `docker-compose.yml` файла при помощи консольной команды `docker-compose` с указанием всех необходимых аргументов для успешного запуска стека приложения. 

#### Ожидаемый результат 

В качестве **результата** проделанной работы, ожидается: 

1. В [основной репозиторий проекта](https://github.com/cardinalit/TTDevOps), оформлен PR,
2. Fork репозиторий содержит все необходимые файлы из задания, 
3. Пользователь может скачать Fork репозиторий для тестирования результатов, 
4. Выполняя последовательно указания из документации по сборке образа и запуску стека сервисов при помощи консольной команды `docker-compose.yml`, пользователь открывает браузер, и перейдя по адресу `http://localhost:8000`, видит загрузку приветственного окна, как представлено на скриншоте в первом блоке задания, 
5. Все сервисы в рамках одного `docker-compose.yml` инкапсулированы в одном сетевом контуре, и только веб-сервер имеет проброс порта на хост `:8000`, 
6. Связь между сервисами обеспечивается по средствам использования имен сервисов и сохранена четкая схема соединения `HTTP (1) <--> HTTP (2) <--> FastCGI (3)`. 

## Система оценки результата

Оценка результатов проходит в соответствии с установленными правилами внутри отдела.  
Каждый шаг задания может быть оценен от двух до пяти баллов, где: 

* **2** - шаг не выполнен,
* **3** - шаг выполнен, но не полностью, самостоятельное тестирование после исполнения - не проводилось, при повторе действий в соответствии с предоставленной документацией, появляются ошибки, блокирующие дальнейшее исполнение, 
* **4** - шаг выполнен, имеются синтаксические, стилистические ошибки, неточности в написании конструкций или использования инструкций для сборки образа и запуска контейнера, 
* **5** - шаг выполнен полностью. Ошибки не возникают, никакое действие не блокирует следующее, имеются рекомендации. 

По каждому баллу отдельно оценивается общая подготовленность и соответствие заявленным знаниям. Исполнитель получит текстовый документ в формате `*.pdf`, где будет оценен каждый из пунктов задания, дан комментарий и обоснование оценки.

## Запуск приложения
1. Сделать клон репозитория с кодом приложения: ``git clone https://github.com/1kan0bi/TTDevOps`` 
2. Перейти в папку с проектом: ``cd TTDevOps`` 
3. Скопировать, переименовать и при необходимости изменить файл конфигурации **.env.example**: ``mv .env.example .env``
3. Собрать образ приложения: ``docker-compose build app``
4. Запустить приложение: ``docker-compose up -d``
5. Установить зависимости приложения: ``docker-compose exec app composer install``
6. Сгенерировать ключ безопасности: ``docker-compose exec app php artisan key:generate``
7. Проверить работу приложения: ``curl localhost:8000``

## P.S.
Я запустил приложение в облаке, можете его посмотреть по [ссылке](http://droplet.devops.rebrain.srwx.net:8000/).
