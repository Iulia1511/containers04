# Лабораторная работа №4
## Цель работы
* Выполнив данную работу студент сможет подготовить образ контейнера для запуска веб-сайта на базе Apache HTTP Server + PHP (mod_php) + MariaDB.

## Задание
* Создать Dockerfile для сборки образа контейнера, который будет содержать веб-сайт на базе Apache HTTP Server + PHP (mod_php) + MariaDB. База данных MariaDB должна храниться в монтируемом томе. Сервер должен быть доступен по порту 8000.
* Установить сайт WordPress. Проверить работоспособность сайта.

## Образ
![1](https://github.com/Iulia1511/containers04/assets/159126852/682b58b8-444f-4dd6-93bc-65d481faaa41)
![2](https://github.com/Iulia1511/containers04/assets/159126852/30c4e621-d795-4e55-b121-c29e6340d033)
## DOCKERFILE 
![image](https://github.com/Iulia1511/containers04/assets/159126852/b1ef73be-b5b7-4690-bf65-f394fc0f2c84)
## Скопируйте из контейнера файлы конфигурации apache2, php, mariadb в папку files/ на компьютере. Для этого, в контексте проекта, выполните команды:
![4](https://github.com/Iulia1511/containers04/assets/159126852/5c7b590b-b222-4bd3-85a5-65ae69ada35a)
## Остановить и удалить
![5](https://github.com/Iulia1511/containers04/assets/159126852/b89ef092-8a86-44af-acb9-a4403d9952f0)
## Настройка конфигурационных файлов
* Конфигурационный файл apache2
* Откройте файл files/apache2/000-default.conf, найдите строку #ServerName www.example.com и замените её на ServerName localhost.
* Найдите строку ServerAdmin webmaster@localhost и замените в ней почтовый адрес на свой.
* После строки DocumentRoot /var/www/html добавьте следующие строки:
* DirectoryIndex index.php index.html
* Сохраните файл и закройте.
  ![6](https://github.com/Iulia1511/containers04/assets/159126852/e6c0c338-e67f-4aaf-93fc-6b2803bdea71)
![7](https://github.com/Iulia1511/containers04/assets/159126852/dc081553-215d-455a-b880-744a2504a36e)

## Конфигурационный файл php
* Откройте файл files/php/php.ini, найдите строку ;error_log = php_errors.log и замените её на error_log = /var/log/php_errors.log.

*Настройте параметры memory_limit, upload_max_filesize, post_max_size и max_execution_time следующим образом:

*memory_limit = 128M
*upload_max_filesize = 128M
*post_max_size = 128M
*max_execution_time = 120
*Сохраните файл и закройте.
![8](https://github.com/Iulia1511/containers04/assets/159126852/74e513ed-a304-4664-9d83-2370c2d654af)
![9](https://github.com/Iulia1511/containers04/assets/159126852/05f8ace3-bc71-44b1-9476-a1a0469a31ee)
* и так далее...
## Конфигурационный файл mariadb
* Откройте файл files/mariadb/50-server.cnf, найдите строку #log_error = /var/log/mysql/error.log и раскомментируйте её.
*Сохраните файл и закройте.

![10](https://github.com/Iulia1511/containers04/assets/159126852/3f4555d3-ef01-4f78-9d32-6f008c32d7a9)
## Создание скрипта запуска
* Создайте в папке files папку supervisor и файл supervisord.conf со следующим содержимым:
![11](https://github.com/Iulia1511/containers04/assets/159126852/65f0820e-1e91-4949-8b8a-41795b63df64)
## Создание Dockerfile
![12](https://github.com/Iulia1511/containers04/assets/159126852/bb3e9ab1-a9f1-40ab-a168-d9a9b61e4863)
## Создание базы данных и пользователя
* mysql
* CREATE DATABASE wordpress;
* CREATE USER 'wordpress'@'localhost' IDENTIFIED BY 'wordpress';
* GRANT ALL PRIVILEGES ON wordpress.* TO 'wordpress'@'localhost';
* FLUSH PRIVILEGES;
* EXIT;
  
![14](https://github.com/Iulia1511/containers04/assets/159126852/be11b11a-a979-4356-aeb4-718eedd96474)
## Создание файла конфигурации WordPress
![15](https://github.com/Iulia1511/containers04/assets/159126852/ed43a35b-c5c6-4fdf-b109-317175fa4ce1)
## Добавление файла конфигурации WordPress в Dockerfile
![16](https://github.com/Iulia1511/containers04/assets/159126852/9d58fe2e-fef2-452d-80d4-27fd4935e7d3)
## Далее запускаем и тестируем.

# Ответы на вопросы
### Измененные файлы конфигурации:
* Конфигурационные файлы для Apache2, PHP и MariaDB были изменены.

### Инструкция DirectoryIndex в файле конфигурации apache2:
* Она указывает, какой файл будет открыт по умолчанию, если в URL указан только каталог.

### Файл wp-config.php:
* Это файл конфигурации WordPress, в котором хранятся настройки базы данных, безопасности и другие параметры.

### Параметр post_max_size в файле конфигурации PHP:
* Он устанавливает максимальный размер данных, которые PHP может принять от клиента через POST-запросы.

### Недостатки образа контейнера:
* Не установлен пароль для базы данных MariaDB.
* Нет механизма автоматических обновлений.












