# ЛР - 1
## Задание 1
### Раздел «Management» (Управление)

2. **Раздел «Client Connections»**. Позволяет просматривать список всех активных подключений к серверу MySQL в реальном времени.
    
    - Отображение идентификатора потока (Thread ID), имени пользователя, хоста и выполняемого в данный момент SQL-запроса.
        
    - Возможность принудительного завершения зависших или нежелательных сессий (кнопка «Kill Connection»).
        
3. **Раздел «Users and Privileges»**. Централизованный интерфейс для управления безопасностью.
    
    - Добавление и удаление учетных записей пользователей.
        
    - Настройка глобальных прав доступа и специфических привилегий для конкретных схем (баз данных).
        
    - Управление аутентификацией и лимитами ресурсов (например, макс. количество запросов в час).
        
4. **Раздел «Data Export / Data Import»**. Инструменты для создания резервных копий и восстановления данных.
    
    - Экспорт структуры таблиц и данных в логические SQL-дампы.
        
    - Импорт данных из внешних SQL-файлов или папок проекта.
### Раздел «Instance» (Экземпляр БД)

Этот раздел предназначен для непосредственного взаимодействия с программной и системной частью сервера MySQL.

1. **Раздел «Startup / Shutdown»**. Позволяет управлять состоянием службы сервера.
    
    - Остановка (Stop) и запуск (Start) сервера без необходимости использовать командную строку ОС.
        
    - Просмотр текущего статуса выполнения процесса.
        
2. **Раздел «Server Logs»**. Предоставляет доступ к текстовым файлам журналов для диагностики.
    
    - Просмотр **Error Log** (ошибки запуска и работы).
        
    - Просмотр **General Log** (запись всех выполненных запросов, если включено).
        
    - Просмотр **Slow Query Log** (запросы, превышающие заданный порог времени выполнения).
        
3. **Раздел «Configuration»**. Редактор системных переменных (файл my.cnf или my.ini).
    
    - Настройка параметров памяти (например, innodb_buffer_pool_size).
        
    - Изменение сетевых настроек и параметров кодировок.
        
    - Валидация изменений перед перезапуском сервера.

### Раздел «Performance» (Производительность)

Раздел предназначен для мониторинга нагрузки и выявления «узких мест» в работе базы данных.

1. **Раздел «Performance Dashboard»**. Визуальная панель с графиками состояния сервера в реальном времени.
    
    - Статистика сетевого трафика (Network Traffic).
        
    - Активность операций чтения/записи на диске (File I/O).
        
    - Статистика попадания в кэш (Buffer Pool Usage) и использование CPU.
        
2. **Раздел «Performance Reports»**. Набор детализированных отчетов на основе данных из performance_schema.
    
    - Анализ наиболее «затратных» запросов (Statement Analysis).
        
    - Отчеты об индексах: поиск неиспользуемых индексов или таблиц, где индексы отсутствуют.
        
    - Анализ ожидания ввода-вывода (I/O Wait Analysis).
        
3. **Раздел «Performance Schema Setup»**. Тонкая настройка инструментов мониторинга.
    
    - Включение и выключение различных «инструментов» и «потребителей» данных для сбора статистики.
        
    - Выбор профиля мониторинга (от минимального до максимально подробного).

## Задание 3
```SQL
CREATE TABLE simpledb.users (`
  `id INT NOT NULL,`
  `name VARCHAR(45) NOT NULL,`
  `email VARCHAR(45) NOT NULL,`
  `PRIMARY KEY (id),`
  `UNIQUE INDEX email_UNIQUE (email ASC) VISIBLE);
```
## Задание 4
```SQL
INSERT INTO `simpledb`.`users` (`id`, `name`, `email`) VALUES ('1', 'Александр', 'a.volkov@example.com');
INSERT INTO `simpledb`.`users` (`id`, `name`, `email`) VALUES ('2', 'Мария', 'mery_kuz92@provider.net');
INSERT INTO `simpledb`.`users` (`id`, `name`, `email`) VALUES ('3', 'Дмитрий', 'dmitry.sokolov@techmail.org');
```

```SQL
UPDATE `simpledb`.`users` SET `email` = 'volkov@example.com' WHERE (`id` = '1');
```
## Задание 5
### Поле created: TIMESTAMP и CURRENT_TIMESTAMP()

- **Тип TIMESTAMP** используется для хранения даты и времени. Его особенность - автоматическая привязка к часовому поясу сервера.
    
- **Значение CURRENT_TIMESTAMP()** означает автоматическую инициализацию: при создании записи сервер сам фиксирует текущее время.
    
- **Вывод:** Это избавляет пользователя (или разработчика) от необходимости вводить дату вручную - база данных делает это сама в момент регистрации.
### Поля NULL

Для пользователей, ценящих приватность, следующие поля определены как **NULL** (необязательные):

- **postal**, **bday**, **gender** - личная информация, которая не влияет на работу аккаунта. Если пользователь не хочет их указывать, в базе зафиксируется «пустота» (NULL).
    
- **rating** - может отсутствовать у новичков.
    

**Обязательными (NOT NULL)** остаются только:

- **id** - для технической уникальности.
    
- **email** - для связи и авторизации.
    
- **created** - заполняется системой автоматически.


```SQL
CREATE TABLE `users` (
  `id` int NOT NULL,
  `name` varchar(50) NOT NULL,
  `email` varchar(45) NOT NULL,
  `postal` varchar(10) DEFAULT NULL,
  `gender` enum('M','F') NOT NULL,
  `bday` date DEFAULT NULL,
  `created` timestamp NULL DEFAULT CURRENT_TIMESTAMP,
  `rating` float NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `email_UNIQUE` (`email`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb3;
```
## Задание 7
```SQL
/*
-- Query: SELECT * FROM simpledb.users
LIMIT 0, 1000

-- Date: 2026-02-11 12:33
*/
INSERT INTO `` (`id`,`name`,`email`,`postal`,`gender`,`bday`,`created`,`rating`) VALUES (1,'Александр','volkov@example.com','125794','M','1999-04-22','2026-02-11 12:08:50',1);
INSERT INTO `` (`id`,`name`,`email`,`postal`,`gender`,`bday`,`created`,`rating`) VALUES (2,'Мария','mery_kuz92@provider.net','125325','F','2000-11-12','2026-02-11 12:08:50',1.24);
INSERT INTO `` (`id`,`name`,`email`,`postal`,`gender`,`bday`,`created`,`rating`) VALUES (3,'Дмитрий','dmitry.sokolov@techmail.org','127957','M','1998-01-21','2026-02-11 12:08:50',1.21);
INSERT INTO `` (`id`,`name`,`email`,`postal`,`gender`,`bday`,`created`,`rating`) VALUES (4,'Ekaterina','ekaterina.petrova@outlook.com','145789','F','2000-02-11','2026-02-11 12:29:43',1.123);
INSERT INTO `` (`id`,`name`,`email`,`postal`,`gender`,`bday`,`created`,`rating`) VALUES (5,'Paul','paul@superpochta.ru','123789','M','1998-08-12','2026-02-11 12:29:43',1);
```
## Задание 8
```SQL
CREATE TABLE `simpledb`.`resume` (
  `resumeid` INT NOT NULL AUTO_INCREMENT,
  `userid` INT NOT NULL,
  `title` VARCHAR(100) NOT NULL,
  `skills` TEXT NULL,
  `created` TIMESTAMP NULL DEFAULT CURRENT_TIMESTAMP(),
  PRIMARY KEY (`resumeid`),
  INDEX `userid_idx` (`userid` ASC) VISIBLE,
  CONSTRAINT `userid`
    FOREIGN KEY (`userid`)
    REFERENCES `simpledb`.`users` (`id`)
    ON DELETE CASCADE
    ON UPDATE CASCADE)
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8;
```

## Информация о студенте
Иванов Федор Владиславович, 2 курс, ИВТ-1.2