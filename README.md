# Отчет по лабораторной работе: Запуск контейнера.

## Цель работы
Основы работы с контейнерами Docker, изучить установку и настройку Apache2 в контейнере Ubuntu.

## Задание
1. Создать репозиторий `containers04` и склонировать его на компьютер.
2. Создать в папке `containers04` файл `README.md` с описанием работы.
3. Выполнить команду запуска контейнера Ubuntu.
4. Установить и запустить Apache2 в контейнере.
5. Проверить работу веб-сервера в браузере.
6. Добавить HTML-файл и проверить его отображение.
7. Просмотреть конфигурацию Apache2.
8. Остановить и удалить контейнер.
9. Описать работу команд и привести их результаты.

## Выполнение работы

### 1. Запуск контейнера Ubuntu с портом 8000
```sh
docker run -ti -p 8000:80 --name containers04 ubuntu bash
```
![Снимок экрана 2025-03-09 202017](https://github.com/user-attachments/assets/87958fb5-7a8c-4357-9917-0c09554a84b1)

**Объяснение:** 
- `docker run -ti` – запуск контейнера в интерактивном режиме.
- `-p 8000:80` – проброс порта (локальный порт 8000 перенаправляется на порт 80 контейнера).
- `--name containers04` – имя контейнера.
- `ubuntu bash` – запуск контейнера с образом Ubuntu и открытием оболочки Bash.

### 4. Установка и запуск Apache2
```sh
apt update
apt install apache2 -y
service apache2 start
```
![Снимок экрана 2025-03-09 202140](https://github.com/user-attachments/assets/fcb79149-c2f7-46de-ab0d-90853668d907)
![Снимок экрана 2025-03-09 202200](https://github.com/user-attachments/assets/2ac76c5a-b988-4c4b-b629-cf440aaa55d6)

**Объяснение:** 
- `apt update` – обновляет список пакетов.
- `apt install apache2 -y` – устанавливает веб-сервер Apache2.
- `service apache2 start` – запускает веб-сервер.

### 5. Проверка работы веб-сервера
Открываем в браузере `http://localhost:8000`.

**Ожидаемый результат:** Стандартная стартовая страница Apache2.
![Снимок экрана 2025-03-09 202310](https://github.com/user-attachments/assets/e5631b18-cfd9-4fc1-b58f-2273483729c5)


### 6. Создание HTML-файла
```sh
ls -l /var/www/html/
echo '<h1>Hello, World!</h1>' > /var/www/html/index.html
```
**Объяснение:**
- `ls -l /var/www/html/` – просмотр содержимого папки сайта.
- `echo '<h1>Hello, World!</h1>' > /var/www/html/index.html` – создание HTML-файла.
![Снимок экрана 2025-03-09 202342](https://github.com/user-attachments/assets/18626a8c-a3d7-4310-a712-d6ce56801196)
![Снимок экрана 2025-03-09 202333](https://github.com/user-attachments/assets/c705c4ad-1364-48af-85a3-70b4ddebbc9e)

### 7. Просмотр конфигурации Apache2
```sh
cd /etc/apache2/sites-enabled/
cat 000-default.conf
```
![Снимок экрана 2025-03-09 203220](https://github.com/user-attachments/assets/9b7e10c9-2a19-4e94-bd23-f07341ef63d7)
##### На скриншоте показан конфигурационный файл 000-default.conf веб-сервера Apache2. Этот файл задает параметры для обработки HTTP-запросов, указывая корневую директорию сайта (/var/www/html), путь к логам (error.log и access.log) и настройки виртуального хоста. Конфигурация определяет, как сервер принимает и обрабатывает входящие соединения на порту 80.

### 9. Просмотр контейнеров
```sh
docker ps -a
```

**Вывод в консоли:**
```
CONTAINER ID   IMAGE     COMMAND   CREATED       STATUS       NAMES
123456789abc   ubuntu    "bash"    5 minutes ago   Exited       containers04
```
![Снимок экрана 2025-03-09 203236](https://github.com/user-attachments/assets/9e9e770d-682c-4a1b-9528-9eedfd0ab746)


## Выводы
В ходе работы был развернут контейнер Ubuntu, установлен веб-сервер Apache2, создан и отображен HTML-файл. Освоены основные команды управления контейнерами Docker.
