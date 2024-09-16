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
CREATE TABLE animal_classes ( 
    id INT AUTO_INCREMENT PRIMARY KEY,
    class_name VARCHAR(50) 
);

INSERT INTO animal_classes (Class_name)
VALUES ('Домашние');

INSERT INTO animal_classes (Class_name)
VALUES ('Вьючные');

SELECT * FROM animal_classes;
```
![image](https://github.com/user-attachments/assets/a27bce1a-60f9-4009-8323-1efc77fbd767)
```sql
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





