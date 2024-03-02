# Итоговая контрольная работа

## Информация о проекте

Необходимо организовать систему учета для питомника, в котором живут домашние и вьючные животные.

## Как сдать проект
Для сдачи проекта необходимо создать отдельный общедоступный репозиторий(Github, gitlub, или Bitbucket). Разработку вести в этом репозитории, использовать пул реквесты на изменения. Программа должна запускаться и работать, ошибок при выполнении программы быть не должно. Программа, может использоваться в различных системах, поэтому необходимо разработать класс в виде конструктора.

## Задание
1. Используя команду cat в терминале операционной системы Linux, создать два файла Домашние животные (заполнив файл собаками, кошками, хомяками) и Вьючные животными заполнив файл (Лошадьми, верблюдами и
ослы), а затем объединить их. Просмотреть содержимое созданного файла. Переименовать файл, дав ему новое имя (Друзья человека).

![Task 1](https://github.com/Dmitri54/Pet_registry/blob/main/Screen_shots/Pet_registry01.jpg)

2. Создать директорию, переместить файл туда.

![Task 2](https://github.com/Dmitri54/Pet_registry/blob/main/Screen_shots/Pet_registry02.jpg)

3. Подключить дополнительный репозиторий MySQL. Установить любой пакет из этого репозитория.

![Task 3.1](https://github.com/Dmitri54/Pet_registry/blob/main/Screen_shots/Pet_registry03.1.jpg)
![Task 3.2](https://github.com/Dmitri54/Pet_registry/blob/main/Screen_shots/Pet_registry03.2.jpg)

4. Установить и удалить deb-пакет с помощью dpkg.

![Task 4](https://github.com/Dmitri54/Pet_registry/blob/main/Screen_shots/Pet_registry04.jpg)

5. Выложить [историю команд](https://github.com/Dmitri54/Pet_registry/blob/main/HistoryCommandsUbuntuTerminal.md) в терминале ubuntu.
6. Нарисовать [диаграмму](https://github.com/Dmitri54/Pet_registry/blob/main/Task_06_diagram.drawio), в которой есть класс родительский класс, домашние животные и вьючные животные, в составы которых в случае домашних животных войдут классы: собаки, кошки, хомяки, а в класс вьючные животные войдут: Лошади, верблюды и ослы.

![Task 6](https://github.com/Dmitri54/Pet_registry/blob/main/Screen_shots/Pet_registry06.jpg)

7. В подключенном MySQL репозитории создать базу данных “Друзья человека”.
``` sql
CREATE DATABASE Human_friends;
```

8. Создать таблицы с иерархией из диаграммы в БД.
``` sql
CREATE SCHEMA `Human_friends` ;
USE Human_friends;

CREATE TABLE animal_classes
(	
	Id INT AUTO_INCREMENT PRIMARY KEY,
    Class_name VARCHAR(20)
);

INSERT INTO animal_classes (Class_name)
VALUES ('вьючные'),
('домашние');

CREATE TABLE home_animals
(
	Id INT AUTO_INCREMENT PRIMARY KEY,
    Genus_name VARCHAR(20),
    Class_id INT,
    FOREIGN KEY (Class_id) REFERENCES animal_classes (Id) ON DELETE CASCADE ON UPDATE CASCADE 
);

INSERT INTO home_animals (Genus_name, Class_id)
VALUES ('Собаки', 2),
('Кошки', 2),
('Хомяки', 2);

CREATE TABLE pack_animals
(
	Id INT AUTO_INCREMENT PRIMARY KEY,
    Genus_name VARCHAR(20),
    Class_id INT,
    FOREIGN KEY (Class_id) REFERENCES animal_classes (Id) ON DELETE CASCADE ON UPDATE CASCADE
);

INSERT INTO pack_animals (Genus_name, Class_id)
VALUES ('Лошади', 1),
('Верблюды', 1),
('Ослы', 1);
```

9. Заполнить низкоуровневые таблицы именами(животных), командами которые они выполняют и датами рождения.
``` sql
CREATE TABLE cats 
(
	Id INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(20),
    Birthday DATE,
    Commands VARCHAR(50),
    Genus_id INT,
    FOREIGN KEY (Genus_id) REFERENCES home_animals (Id) ON DELETE CASCADE ON UPDATE CASCADE
);

INSERT INTO cats (Name, Birthday, Commands, Genus_id)
VALUES ('Мурка', '2017-05-11', 'кс-кс-кс', 1),
('Кузя', '2018-01-15', 'куз-куз', 1),
('Лапа', '2019-03-01', '', 1);

CREATE TABLE dogs
(
	Id INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(20),
    Birthday DATE,
    Commands VARCHAR(50),
    Genus_id INT,
    FOREIGN KEY (Genus_id) REFERENCES home_animals (Id) ON DELETE CASCADE ON UPDATE CASCADE
); 

INSERT INTO dogs (Name, Birthday, Commands, Genus_id)
VALUES ('Шарик', '2020-08-01', 'ко мне, сидеть, лежать', 2),
('Даша', '2021-01-20', 'ко мне, сидеть, лежать, лапу, голос', 2),
('Дуся', '2016-04-29', 'место, фу!', 2),
('Нора', '2010-02-01', 'лапу, голос, место', 2);

CREATE TABLE hamsters 
(
	Id INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(20),
    Birthday DATE,
    Commands VARCHAR(50),
    Genus_id INT,
    FOREIGN KEY (Genus_id) REFERENCES home_animals (Id) ON DELETE CASCADE ON UPDATE CASCADE
);

INSERT INTO hamsters (Name, Birthday, Commands, Genus_id)
VALUES ('Хомяк', '2019-01-01', '', 3),
('Серега', '2020-12-04', 'Чужой', 3),
('Пух', '2021-11-01', '', 3),
('Луна', '2022-06-09', '', 3);

CREATE TABLE horses 
(
	Id INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(20),
    Birthday DATE,
    Commands VARCHAR(50),
    Genus_id INT,
    FOREIGN KEY (Genus_id) REFERENCES pack_animals (Id) ON DELETE CASCADE ON UPDATE CASCADE
);

INSERT INTO horses (Name, Birthday, Commands, Genus_id)
VALUES ('Ангел', '2019-10-01', 'вперёд, хоп, шагом', 1),
('Молния', '2018-01-20', 'рысь, хоп, шагом, тише, стой', 1),
('Буран', '2020-06-04', 'шагом, стой', 1),
('Гром', '2022-05-08', 'вперёд, стой, шагом', 1);

CREATE TABLE donkeys 
(
	Id INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(20),
    Birthday DATE,
    Commands VARCHAR(50),
    Genus_id INT,
    FOREIGN KEY (Genus_id) REFERENCES pack_animals (Id) ON DELETE CASCADE ON UPDATE CASCADE
);

INSERT INTO donkeys (Name, Birthday, Commands, Genus_id)
VALUES ('Гранат', '2020-01-01', '', 1),
('Бомбай', '2015-01-01', '', 1),
('Жак', '2018-08-21', '', 1),
('Брюс', '2021-10-07', 'ИА-ИА', 1);

CREATE TABLE camels 
(
	Id INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(20),
    Birthday DATE,
    Commands VARCHAR(50),
    Genus_id INT,
    FOREIGN KEY (Genus_id) REFERENCES pack_animals (Id) ON DELETE CASCADE ON UPDATE CASCADE
);

INSERT INTO camels (Name, Birthday, Commands, Genus_id)
VALUES ('Жетем', '2020-01-11', 'КХХ', 3),
('Лила', '2015-07-03', 'ГИТ!, КАШ!', 3),
('Хлоя', '2018-12-02', 'ДУРР!, ЦОК-ЦОК, ХАП-ХАП-ХАП', 3),
('Омлет', '2021-12-08', 'ДУРР!, ГИТ!, КАШ!', 3);
```

10. Удалив из таблицы верблюдов, т.к. верблюдов решили перевезти в другой питомник на зимовку.Объединить таблицы лошади, и ослы в одну таблицу.
``` sql
SET SQL_SAFE_UPDATES = 0;
DELETE FROM camels;

SELECT Name, Birthday, Commands FROM horses
UNION SELECT Name, Birthday, Commands FROM donkeys;
```

11. Создать новую таблицу “молодые животные” в которую попадут все животные старше 1 года, но младше 3 лет и в отдельном столбце с точностью до месяца подсчитать возраст животных в новой таблице.
``` sql
CREATE TEMPORARY TABLE animals AS
SELECT*, 'Кошки' AS genus FROM cats
UNION SELECT*, 'Собаки' AS genus FROM dogs
UNION SELECT*, 'Хомяки' AS genus FROM hamsters
UNION SELECT*, 'Лошади' AS genus FROM horses
UNION SELECT*, 'Ослы' AS genus FROM donkeys;

CREATE TABLE yang_animals AS
SELECT Name, Birthday, Commands, genus, TIMESTAMPDIFF(MONTH, Birthday, CURDATE()) AS Age_in_month
FROM animals WHERE Birthday BETWEEN ADDDATE(CURDATE(), INTERVAL - 3 YEAR) AND ADDDATE(CURDATE(), INTERVAL - 1 YEAR);

SELECT* FROM yang_animals;
```

12. Объединить все таблицы в одну, при этом сохраняя поля, указывающие на прошлую принадлежность к старым таблицам.
``` sql
SELECT c.Name, c.Birthday, c.Commands, ha.Genus_name, ya.Age_in_month
FROM cats c
LEFT JOIN yang_animals ya ON ya.Name = c.Name
LEFT JOIN home_animals ha ON ha.Id = c.Genus_id
UNION
SELECT d.Name, d.Birthday, d.Commands, ha.Genus_name, ya.Age_in_month
FROM dogs d
LEFT JOIN yang_animals ya ON ya.Name = d.Name
LEFT JOIN home_animals ha ON ha.Id = d.Genus_id
UNION
SELECT hm.Name, hm.Birthday, hm.Commands, ha.Genus_name, ya.Age_in_month
FROM hamsters hm
LEFT JOIN yang_animals ya ON ya.Name = hm.Name
LEFT JOIN home_animals ha ON ha.Id = hm.Genus_id
UNION
SELECT h.Name, h.Birthday, h.Commands, pa.Genus_name, ya.Age_in_month
FROM horses h
LEFT JOIN yang_animals ya ON ya.Name = h.Name
LEFT JOIN pack_animals pa ON pa.Id = h.Genus_id
UNION
SELECT d.Name, d.Birthday, d.Commands, pa.Genus_name, ya.Age_in_month
FROM donkeys d
LEFT JOIN yang_animals ya ON ya.Name = d.Name
LEFT JOIN pack_animals pa ON pa.Id = d.Genus_id;
```

13. Создать класс с Инкапсуляцией методов и наследованием по диаграмме.
14. Написать программу, имитирующую работу реестра домашних животных. 
В программе должен быть реализован следующий функционал:
14.1 Завести новое животное;
14.2 определять животное в правильный класс;
14.3 увидеть список команд, которое выполняет животное;
14.4 обучить животное новым командам;
14.5 Реализовать навигацию по меню.
15. Создайте класс Счетчик, у которого есть метод add(), увеличивающий̆ значение внутренней̆ int переменной̆ на 1 при нажатие “Завести новое животное” Сделайте так, чтобы с объектом такого типа можно было работать в блоке try-with-resources. Нужно бросить исключение, если работа с объектом
типа счетчик была не в ресурсном try и/или ресурс остался открыт. Значение считать в ресурсе try, если при заведения животного заполнены все поля.