# final_work
1. Используя команду cat в терминале операционной системы Linux, создать
два файла Домашние животные (заполнив файл собаками, кошками,
хомяками) и Вьючные животными заполнив файл Лошадьми, верблюдами и
ослы), а затем объединить их. Просмотреть содержимое созданного файла.
Переименовать файл, дав ему новое имя (Друзья человека).

![image](https://github.com/user-attachments/assets/fdc1dcca-ca8b-4175-9be5-df16100e4d2b)

2. Создать директорию, переместить файл туда.
![image](https://github.com/user-attachments/assets/4776aaa1-c54f-4d27-85af-a50de9eb3d43)

3. Подключить дополнительный репозиторий MySQL. Установить любой пакет
из этого репозитория.
![image](https://github.com/user-attachments/assets/ff78716c-1375-473f-a090-95baaa224324)
![image](https://github.com/user-attachments/assets/8cbf61e0-a666-47bf-8076-9a83bacf9c68)

4. Установить и удалить deb-пакет с помощью dpkg.

![image](https://github.com/user-attachments/assets/ffd47cdd-6a4f-4cde-8452-2d4e40506b8d)

5. Выложить историю команд в терминале ubuntu

![image](https://github.com/user-attachments/assets/6440da6d-cf63-458d-b1ef-539d39e3ef90)

6. Нарисовать диаграмму, в которой есть класс родительский класс, домашние
животные и вьючные животные, в составы которых в случае домашних
животных войдут классы: собаки, кошки, хомяки, а в класс вьючные животные
войдут: Лошади, верблюды и ослы).
![Диаграмма без названия drawio](https://github.com/user-attachments/assets/67c2f6f9-e3ee-41c6-a666-d71166d8228c)

7. В подключенном MySQL репозитории создать базу данных “Друзья
человека”
![image](https://github.com/user-attachments/assets/12b0ef81-2b32-475d-afc9-584632263f8a)

8. Создать таблицы с иерархией из диаграммы в БД
```sql
DROP TABLE IF EXISTS animal_classes;
CREATE TABLE animal_classes ( 
    id INT AUTO_INCREMENT PRIMARY KEY,
    class_name VARCHAR(50) 
);

INSERT INTO animal_classes (сlass_name)
VALUES ('Домашние');

INSERT INTO animal_classes (сlass_name)
VALUES ('Вьючные');

SELECT * FROM animal_classes;
```
![image](https://github.com/user-attachments/assets/a27bce1a-60f9-4009-8323-1efc77fbd767)
```sql

DROP TABLE IF EXISTS pets_animals;
CREATE TABLE pets_animals (
    `id` INT AUTO_INCREMENT PRIMARY KEY,
     animal_species VARCHAR (50),
     class_id INT,
     FOREIGN KEY (class_id) REFERENCES animal_classes (id) ON DELETE CASCADE ON UPDATE CASCADE
);

INSERT INTO pets_animals (animal_species, class_id)
VALUES ('Кошки', 2),
('Собаки', 2),  
('Хомяки', 2);

DROP TABLE IF EXISTS packs_animals;
CREATE TABLE packs_animals (
 `id` INT AUTO_INCREMENT PRIMARY KEY,
     animal_species VARCHAR (50),
     class_id INT,
     FOREIGN KEY (class_id) REFERENCES animal_classes (id) ON DELETE CASCADE ON UPDATE CASCADE
);

INSERT INTO packs_animals (animal_species, class_id)
VALUES ('Лошади', 1),
('Ослы', 1),  
('Верблюды', 1); 
```
9. Заполнить низкоуровневые таблицы именами(животных), командами которые они выполняют и датами рождения
```sql
DROP TABLE IF EXISTS dogs;
CREATE TABLE dogs (       
    Id INT AUTO_INCREMENT PRIMARY KEY, 
    name VARCHAR(50), 
    birthday DATE,
    commands VARCHAR(50),
    subspecies_id int,
    FOREIGN KEY (subspecies_id) REFERENCES pets_animals (id) ON DELETE CASCADE ON UPDATE CASCADE
);

INSERT INTO dogs (name, birthday, commands, subspecies_id)
VALUES ('Шарик', '2024-05-06', 'Сидеть', 2),
('Матрос', '2024-01-12', 'Дай лапу', 2),  
('Псина', '2024-03-11', 'Фу', 2), 
('Счастливчик', '2022-03-12', 'Кто хороший мальчик?', 2
);

DROP TABLE IF EXISTS cats;
CREATE TABLE cats (       
    Id INT AUTO_INCREMENT PRIMARY KEY, 
    name VARCHAR(50), 
    birthday DATE,
    commands VARCHAR(50),
    subspecies_id int,
    FOREIGN KEY (subspecies_id) REFERENCES pets_animals (id) ON DELETE CASCADE ON UPDATE CASCADE
);

INSERT INTO cats (name, birthday, commands, subspecies_id)
VALUES ('Мурка', '2024-02-06', 'кскс', 1),
('Мурзик', '2023-01-12', 'Иди кушать', 1),  
('Ася', '2021-03-12', 'кскс', 1), 
('Айрис', '2023-06-11', 'Где моя кошечка?', 1
);

DROP TABLE IF EXISTS hamsters;
CREATE TABLE hamsters (       
    id INT AUTO_INCREMENT PRIMARY KEY, 
    name VARCHAR(50), 
    birthday DATE,
    commands VARCHAR(50),
    subspecies_id int,
    FOREIGN KEY (subspecies_id) REFERENCES pets_animals (id) ON DELETE CASCADE ON UPDATE CASCADE
);

INSERT INTO hamsters (name, birthday, commands, subspecies_id)
VALUES ('Мили', '2024-10-03', NULL, 3),
('Степан', '2024-06-09', NULL, 3),  
('Капля', '2021-05-17', NULL, 3), 
('Звезда', '2020-01-09', NULL, 3
);

DROP TABLE IF EXISTS horses;
CREATE TABLE horses (
id INT AUTO_INCREMENT PRIMARY KEY, 
    name VARCHAR(50), 
    birthday DATE,
    commands VARCHAR(50),
    subspecies_id int,
    FOREIGN KEY (subspecies_id) REFERENCES packs_animals (id) ON DELETE CASCADE ON UPDATE CASCADE
);

INSERT INTO horses (name, birthday, commands, subspecies_id)
VALUES ('Левик', '2019-11-03', 'Прууу', 1),
('Бурый', '2022-04-09', 'Бегом', 1),  
('Молниеносец', '2018-05-12', 'Ам Ам', 1), 
('Тайфун', '2020-01-04', 'Стой', 1
);

DROP TABLE IF EXISTS donkeys;
CREATE TABLE donkeys (
id INT AUTO_INCREMENT PRIMARY KEY, 
    name VARCHAR(50), 
    birthday DATE,
    commands VARCHAR(50),
    subspecies_id int,
    FOREIGN KEY (subspecies_id) REFERENCES packs_animals (id) ON DELETE CASCADE ON UPDATE CASCADE
);

INSERT INTO donkeys (name, birthday, commands, subspecies_id)
VALUES ('Мартин', '2019-11-03', 'Стой', 2),
('Зефир', '2022-03-09', 'Иди', 2),  
('Буревестник', '2019-07-12', 'Стой', 2), 
('Пухляш', '2024-02-04', 'Стой', 2
);

DROP TABLE IF EXISTS camels;
CREATE TABLE camels (
id INT AUTO_INCREMENT PRIMARY KEY, 
    name VARCHAR(50), 
    birthday DATE,
    commands VARCHAR(50),
    subspecies_id int,
    FOREIGN KEY (subspecies_id) REFERENCES packs_animals (id) ON DELETE CASCADE ON UPDATE CASCADE
);

INSERT INTO camels (name, birthday, commands, subspecies_id)
VALUES ('Саванна', '2019-11-03', 'Где это мы?', 3),
('Улыбка', '2021-06-05', 'Ищи воду', 3),  
('Жемчужина', '2017-07-06', 'Садись', 3), 
('Песчаник', '2022-04-04', 'Стой', 3
);
```
10. Удалив из таблицы верблюдов, т.к. верблюдов решили перевезти в другой
питомник на зимовку. Объединить таблицы лошади, и ослы в одну таблицу.

```sql
DROP TABLE IF EXISTS camels;
DROP TABLE IF EXISTS horses_donkeys;
CREATE TABLE horses_donkeys (
id INT AUTO_INCREMENT PRIMARY KEY, 
    name VARCHAR(50), 
    birthday DATE,
    commands VARCHAR(50),
    subspecies_id int,
    FOREIGN KEY (subspecies_id) REFERENCES packs_animals (id) ON DELETE CASCADE ON UPDATE CASCADE
);

INSERT INTO horses_donkeys (name, birthday, commands, subspecies_id) SELECT name, birthday, commands, subspecies_id FROM horses;
INSERT INTO horses_donkeys (name, birthday, commands, subspecies_id) SELECT name, birthday, commands, subspecies_id FROM donkeys;
DROP TABLE IF EXISTS horses;
DROP TABLE IF EXISTS donkeys;
```

11.Создать новую таблицу “молодые животные” в которую попадут все
животные старше 1 года, но младше 3 лет и в отдельном столбце с точностью
до месяца подсчитать возраст животных в новой таблице
```sql
DROP TABLE IF EXISTS young_animals;
CREATE TABLE young_animals (
    id int NOT NULL, 
    name VARCHAR(50), 
    birthday DATE,
    commands VARCHAR(50),
    age VARCHAR(50)
);

INSERT INTO young_animals (id, name, birthday, commands, age)
SELECT id, name, birthday, commands,
CONCAT(CAST(TIMESTAMPDIFF(YEAR, birthday, NOW()) AS CHAR), " ЛЕТ ",
CAST(MOD(TIMESTAMPDIFF(MONTH, birthday, NOW()), 12) AS CHAR), " МЕС ") AS age
FROM cats
WHERE TIMESTAMPDIFF(MONTH, birthday, NOW()) BETWEEN 12 AND 36;

INSERT INTO young_animals (id, name, birthday, commands, age)
SELECT id, name, birthday, commands,
CONCAT(CAST(TIMESTAMPDIFF(YEAR, birthday, NOW()) AS CHAR), " ЛЕТ ",
CAST(MOD(TIMESTAMPDIFF(MONTH, birthday, NOW()), 12) AS CHAR), " МЕС ") AS age
FROM dogs
WHERE TIMESTAMPDIFF(MONTH, birthday, NOW()) BETWEEN 12 AND 36;

INSERT INTO young_animals (id, name, birthday, commands, age)
SELECT id, name, birthday, commands,
CONCAT(CAST(TIMESTAMPDIFF(YEAR, birthday, NOW()) AS CHAR), " ЛЕТ ",
CAST(MOD(TIMESTAMPDIFF(MONTH, birthday, NOW()), 12) AS CHAR), " МЕС ") AS age
FROM hamsters
WHERE TIMESTAMPDIFF(MONTH, birthday, NOW()) BETWEEN 12 AND 36;

INSERT INTO young_animals (id, name, birthday, commands, age)
SELECT id, name, birthday, commands,
CONCAT(CAST(TIMESTAMPDIFF(YEAR, birthday, NOW()) AS CHAR), " ЛЕТ ",
CAST(MOD(TIMESTAMPDIFF(MONTH, birthday, NOW()), 12) AS CHAR), " МЕС ") AS age
FROM horses_donkeys
WHERE TIMESTAMPDIFF(MONTH, birthday, NOW()) BETWEEN 12 AND 36;

SELECT * FROM young_animals;
```
![image](https://github.com/user-attachments/assets/1b7a3414-5834-4099-9b3d-22d29b491106)

12. Объединить все таблицы в одну, при этом сохраняя поля, указывающие на
прошлую принадлежность к старым таблицам.
```sql
DROP TABLE IF EXISTS all_animals;
CREATE TABLE all_animals AS
SELECT *, 'horses_donkeys' AS previous_table
FROM horses_donkeys
UNION
SELECT *, 'cats' AS previous_table
FROM cats
UNION
SELECT *, 'dogs' AS previous_table
FROM dogs
UNION
SELECT *, 'hamsters' AS previous_table
FROM hamsters
UNION
SELECT *, 'YoungAnimals' AS previous_table
FROM young_animals;
SELECT * FROM all_animals;
```
![image](https://github.com/user-attachments/assets/af8664f4-a1ea-4b14-90d7-8930432a4b8d)

