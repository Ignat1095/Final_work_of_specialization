# Итоговая контрольная работа

## Информация о проекте
Необходимо организовать систему учета для питомника в котором живут
домашние и вьючные животные.

# Задание
1. Используя команду __cat__ в терминале операционной системы __Linux__, создать два файла __Домашние животные__ (заполнив файл собаками, кошками, хомяками) и __Вьючные животные__, заполнив файл лошадьми, верблюдамии ослы), а затем объединить их. Просмотреть содержимое созданного файла. Переименовать файл, дав ему новое имя __Друзья человека__. 
2. Создать директорию, переместить файл туда.
3. Подключить дополнительный репозиторий __MySQL__. Установить любой пакет из этого репозитория.
4. Установить и удалить __deb__-пакет с помощью __dpkg__.
5. Выложить историю команд в терминале ubuntu
    ![screenshot](https://github.com/Ignat1095/Final_work_of_specialization/blob/main/images/%D0%BF%D0%B5%D1%80%D0%B2%D0%B0%D1%8F%20%D1%87%D0%B0%D1%81%D1%82%D1%8C.PNG)
6. Нарисовать диаграмму, в которой есть класс родительский класс, домашние
животные и вьючные животные, в составы которых в случае домашних
животных войдут классы: собаки, кошки, хомяки, а в класс вьючные животные
войдут: Лошади, верблюды и ослы).

    ![screenshot2](https://github.com/Ignat1095/Final_work_of_specialization/blob/main/images/%D0%94%D0%B8%D0%B0%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%B0%20%D0%B7%D0%B2%D0%B5%D1%80%D0%B5%D0%B9.PNG)
7. В подключенном __MySQL__ репозитории создать базу данных “Друзья
человека”
    ```
    CREATE DATABASE Human_friends;
    ```
8. Создать таблицы с иерархией из диаграммы в БД
    ```
    USE Human_friends;
    CREATE TABLE animal_classes
    (
        Id INT AUTO_INCREMENT PRIMARY KEY, 
        Class_name VARCHAR(20)
    );

    INSERT INTO animal_classes (Class_name)
    VALUES 
    ('вьючные'),
    ('домашние');  


    CREATE TABLE packed_animals
    (
        Id INT AUTO_INCREMENT PRIMARY KEY,
        Genus_name VARCHAR (20),
        Class_id INT,
        FOREIGN KEY (Class_id) REFERENCES animal_classes (Id) ON DELETE CASCADE ON UPDATE CASCADE
    );

    INSERT INTO packed_animals (Genus_name, Class_id)
    VALUES ('Лошади', 1),
    ('Ослы', 1),  
    ('Верблюды', 1); 

    CREATE TABLE home_animals
    (
        Id INT AUTO_INCREMENT PRIMARY KEY,
        Genus_name VARCHAR (20),
        Class_id INT,
        FOREIGN KEY (Class_id) REFERENCES animal_classes (Id) ON DELETE CASCADE ON UPDATE CASCADE
    );

    INSERT INTO home_animals (Genus_name, Class_id)
    VALUES 
    ('Кошки', 2),
    ('Собаки', 2),  
    ('Хомяки', 2); 

    CREATE TABLE cats 
    (       
        Id INT AUTO_INCREMENT PRIMARY KEY, 
        Name VARCHAR(20), 
        Birthday DATE,
        Commands VARCHAR(50),
        Genus_id int,
        Foreign KEY (Genus_id) REFERENCES home_animals (Id) ON DELETE CASCADE ON UPDATE CASCADE
    );
    ```
9. Заполнить низкоуровневые таблицы именами(животных), командами
которые они выполняют и датами рождения.
    ```
    INSERT INTO cats (Name, Birthday, Commands, Genus_id)
    VALUES 
    ('Марса', '2011-01-01', 'кис-кис-кис', 1),
    ('Зара', '2016-01-01', "Мясо!", 1),  
    ('Кефир', '2017-01-01', "", 1); 

    CREATE TABLE dogs 
    (       
        Id INT AUTO_INCREMENT PRIMARY KEY, 
        Name VARCHAR(20), 
        Birthday DATE,
        Commands VARCHAR(50),
        Genus_id int,
        Foreign KEY (Genus_id) REFERENCES home_animals (Id) ON DELETE CASCADE ON   UPDATE CASCADE
    );
    INSERT INTO dogs (Name, Birthday, Commands, Genus_id)
    VALUES ('Зиг', '2020-01-01', 'ко мне, лежать, лапу, голос', 2),
    ('Герцог', '2021-06-12', "сидеть, лежать, лапу", 2),  
    ('Рогоз', '2018-05-01', "сидеть, лежать, лапу, след, фас", 2), 
    ('Спайк', '2021-05-10', "сидеть, лежать, фу, место", 2);

    CREATE TABLE hamsters 
    (       
        Id INT AUTO_INCREMENT PRIMARY KEY, 
        Name VARCHAR(20), 
        Birthday DATE,
        Commands VARCHAR(50),
        Genus_id int,
        Foreign KEY (Genus_id) REFERENCES home_animals (Id) ON DELETE CASCADE ON UPDATE CASCADE
    );
    INSERT INTO hamsters (Name, Birthday, Commands, Genus_id)
    VALUES 
    ('Ириска', '2020-10-12', 'NULL ', 3),
    ('Коржик', '2021-03-12', "NULL ", 3),  
    ('Зефир', '2022-07-11', NULL, 3), 
    ('Конфета', '2022-05-10', NULL, 3);

    CREATE TABLE horses 
    (       
        Id INT AUTO_INCREMENT PRIMARY KEY, 
        Name VARCHAR(20), 
        Birthday DATE,
        Commands VARCHAR(50),
        Genus_id int,
        Foreign KEY (Genus_id) REFERENCES packed_animals (Id) ON DELETE CASCADE ON UPDATE CASCADE
    );
    INSERT INTO horses (Name, Birthday, Commands, Genus_id)
    VALUES 
    ('Гром', '2020-01-12', 'бегом, шагом', 1),
    ('Апполон', '2017-03-12', "бегом, шагом, галоп", 1),  
    ('Ангел', '2016-07-12', "бегом, шагом, галоп, брр", 1), 
    ('Дакар', '2020-11-10', "бегом, шагом, галоп", 1);

    CREATE TABLE donkeys 
    (       
        Id INT AUTO_INCREMENT PRIMARY KEY, 
        Name VARCHAR(20), 
        Birthday DATE,
        Commands VARCHAR(50),
        Genus_id int,
        Foreign KEY (Genus_id) REFERENCES packed_animals (Id) ON DELETE CASCADE ON UPDATE CASCADE
    );
    INSERT INTO donkeys (Name, Birthday, Commands, Genus_id)
    VALUES 
    ('Первый', '2019-04-10', NULL, 2),
    ('Второй', '2020-03-12', "", 2),  
    ('Третий', '2021-07-12', "", 2), 
    ('Четвертый', '2022-12-10', NULL, 2);

    CREATE TABLE camels 
    (       
        Id INT AUTO_INCREMENT PRIMARY KEY, 
        Name VARCHAR(20), 
        Birthday DATE,
        Commands VARCHAR(50),
        Genus_id int,
        Foreign KEY (Genus_id) REFERENCES packed_animals (Id) ON DELETE CASCADE ON UPDATE CASCADE
    );
    INSERT INTO camels (Name, Birthday, Commands, Genus_id)
    VALUES 
    ('Горбатый', '2022-04-10', 'вернись', 3),
    ('Самец', '2019-03-12', "остановись", 3),  
    ('Сифон', '2015-07-12', "повернись", 3), 
    ('Борода', '2022-12-10', "улыбнись", 3);
    ```
10. Удалив из таблицы верблюдов, т.к. верблюдов решили перевезти в другой
питомник на зимовку. Объединить таблицы лошади, и ослы в одну таблицу.
    ```
    SET SQL_SAFE_UPDATES = 0;
    DELETE FROM camels;

    SELECT Name, Birthday, Commands FROM horses
    UNION SELECT  Name, Birthday, Commands FROM donkeys;
    ```
11. Создать новую таблицу “молодые животные” в которую попадут все
животные старше 1 года, но младше 3 лет и в отдельном столбце с точностью
до месяца подсчитать возраст животных в новой таблице.
    ```
    CREATE TEMPORARY TABLE animals AS 
    SELECT *, 'Лошади' AS genus FROM horses
    UNION SELECT *, 'Ослы' AS genus FROM donkeys
    UNION SELECT *, 'Собаки' AS genus FROM dogs
    UNION SELECT *, 'Кошки' AS genus FROM cats
    UNION SELECT *, 'Хомяки' AS genus FROM hamsters;

    CREATE TABLE young_animal AS
    SELECT Name, Birthday, Commands, genus, TIMESTAMPDIFF(MONTH, Birthday, CURDATE()) AS Age_in_month
    FROM animals WHERE Birthday BETWEEN ADDDATE(curdate(), INTERVAL -3 YEAR) AND ADDDATE(CURDATE(), INTERVAL -1 YEAR);

    SELECT * FROM young_animal;
    ```
12. Объединить все таблицы в одну, при этом сохраняя поля, указывающие на
прошлую принадлежность к старым таблицам.
    ```
    SELECT h.Name, h.Birthday, h.Commands, pa.Genus_name, yo.Age_in_month 
    FROM horses h
    LEFT JOIN young_animal ya ON ya.Name = h.Name
    LEFT JOIN packed_animals pa ON pa.Id = h.Genus_id
    UNION 
    SELECT d.Name, d.Birthday, d.Commands, pa.Genus_name, ya.Age_in_month 
    FROM donkeys d 
    LEFT JOIN young_animal ya ON ya.Name = d.Name
    LEFT JOIN packed_animals pa ON pa.Id = d.Genus_id
    UNION
    SELECT c.Name, c.Birthday, c.Commands, ha.Genus_name, ya.Age_in_month 
    FROM cats c
    LEFT JOIN young_animal ya ON ya.Name = c.Name
    LEFT JOIN home_animals ha ON ha.Id = c.Genus_id
    UNION
    SELECT d.Name, d.Birthday, d.Commands, ha.Genus_name, ya.Age_in_month 
    FROM dogs d
    LEFT JOIN young_animal ya ON ya.Name = d.Name
    LEFT JOIN home_animals ha ON ha.Id = d.Genus_id
    UNION
    SELECT hm.Name, hm.Birthday, hm.Commands, ha.Genus_name, ya.Age_in_month 
    FROM hamsters hm
    LEFT JOIN young_animal ya ON ya.Name = hm.Name
    LEFT JOIN home_animals ha ON ha.Id = hm.Genus_id;
    ```
    ![sql](https://github.com/Ignat1095/Final_work_of_specialization/blob/main/images/sql.PNG)
13. Создать класс с Инкапсуляцией методов и наследованием по диаграмме.
14. Написать программу, имитирующую работу реестра домашних животных. В программе должен быть реализован следующий функционал:
* Завести новое животное
* Определять животное в правильный класс
* Увидеть список команд, которое выполняет животное
* Обучить животное новым командам
* Реализовать навигацию по меню
15. Создайте класс Счетчик, у которого есть метод __add()__, увеличивающий значение внутренней int переменной на 1 при нажатии “Завести новое животное”. 
Сделайте так, чтобы с объектом такого типа можно было работать в
блоке __try-with-resources__. Нужно бросить исключение, если работа с объектом,
типа счетчик была не в ресурсном try и/или ресурс остался открыт. Значение
считать в ресурсе try, если при заведения животного заполнены все поля.

