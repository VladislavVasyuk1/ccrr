# Задание №1
### Используя команду cat в терминале операционной системы Linux, создать два файла Домашние животные (заполнив файл собаками, кошками, хомяками) и Вьючные животными заполнив файл Лошадьми, верблюдами и ослы), а затем объединить их. Просмотреть содержимое созданного файла. Переименовать файл, дав ему новое имя (Друзья человека).
<pre>
mkdir test
cd test
ls

cat <<EOT >> pets.txt
cat
dog
hamster
EOT

cat <<EOT >> pack_animals.txt  
horse  
camel  
donkey
EOT

cat pets.txt pack_animals.txt > animals.txt

mv animals.txt human_friends.txt  
</pre>
# Задание №2
### Создать директорию, переместить файл туда.
<pre>
mkdir newdir
mv human_friends.txt newdir
</pre>
# Задание №3
### Подключить дополнительный репозиторий MySQL. Установить любой пакет из этого репозитория.
<pre>
wget -c https://dev.mysql.com/get/mysql-apt-config_0.8.30-1_all.deb
sudo dpkg -i mysql-apt-config_0.8.30-1_all.deb

sudo apt update
sudo apt install mysql-server
</pre>
# Задание №4
### Установить и удалить deb-пакет с помощью dpkg.
<pre>
wget -c http://ftp.ru.debian.org/debian/pool/main/n/nginx/nginx_1.22.1-9_amd64.deb
sudo dpkg -i nginx_1.22.1-9_amd64.deb
sudo apt-get install -f
sudo dpkg -r nginx nginx-common
</pre>
# Задание №5
### Выложить историю команд в терминале ubuntu
<pre>
   91  mkdir test
   92  cd test
   93  ls
   94  cat <<EOT >> pets.txt
   95  cat
   96  dog
   97  hamster
   98  EOT
   99  cat pets.txt
  100  cat <<EOT >> pack_animals.txt
  101  horse
  102  camel
  103  donkey
  104  EOT
  105  cat pack_animals.txt
  106  cat pets.txt pack_animals.txt > animals.txt
  107  cat animals.txt
  108  mv animals.txt human_friends.txt
  109  ls
  110  mkdir newdir
  111  mv human_friends.txt newdir
  112  ls
  113  ls newdir
  114  wget -c https://dev.mysql.com/get/mysql-apt-config_0.8.30-1_all.deb
  115  sudo dpkg -i mysql-apt-config_0.8.30-1_all.deb
  116  sudo apt update
  117  sudo apt install mysql-server
  118  systemctl status mysql
  119  wget -c http://ftp.ru.debian.org/debian/pool/main/n/nginx/nginx_1.22.1-9_amd64.deb
  120  sudo dpkg -i nginx_1.22.1-9_amd64.deb
  121  sudo apt-get install -f
  122  sudo dpkg -r nginx nginx-common
  123  sudo apt-get install -f
  124  sudo dpkg -r nginx nginx-common
  125  history 40
  126  history
</pre>
# Задание №6
###  Нарисовать диаграмму, в которой есть класс родительский класс, домашние животные и вьючные животные, в составы которых в случае домашних животных войдут классы: собаки, кошки, хомяки, а в класс вьючные животные войдут: Лошади, верблюды и ослы.
# Задание №7
### В подключенном MySQL репозитории создать базу данных “Друзья человека”
<pre>
CREATE database HumanFriends;
</pre>
# Задание №8
###  Создать таблицы с иерархией из диаграммы в БД
<pre>
DROP TABLE IF EXISTS HumanFriends;
CREATE TABLE HumanFriends (
    id_human_friend INT AUTO_INCREMENT PRIMARY KEY,
    type_human_friend VARCHAR(255)
);

DROP TABLE IF EXISTS Pets;
CREATE TABLE Pets (
    id_pet INT AUTO_INCREMENT PRIMARY KEY,
    type_pet VARCHAR(255),
    id_human_friend INT,
    FOREIGN KEY (id_human_friend) REFERENCES HumanFriends(id_human_friend)
);

DROP TABLE IF EXISTS PackAnimals;
CREATE TABLE PackAnimals (
    id_pack_animal INT AUTO_INCREMENT PRIMARY KEY,
    type_pack_animal VARCHAR(255),
    id_human_friend INT,
    FOREIGN KEY (id_human_friend) REFERENCES HumanFriends(id_human_friend)
);

DROP TABLE IF EXISTS Cats;
CREATE TABLE Cats (
    id_cat INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255),
    birth_day DATE,
    commands TEXT,
    id_pet INT,
    FOREIGN KEY (id_pet) REFERENCES Pets(id_pet)
);

DROP TABLE IF EXISTS Dogs;
CREATE TABLE Dogs (
    id_dog INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255),
    birth_day DATE,
    commands TEXT,
    id_pet INT,
    FOREIGN KEY (id_pet) REFERENCES Pets(id_pet)
);

DROP TABLE IF EXISTS Hamsters;
CREATE TABLE Hamsters (
    id_hamster INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255),
    birth_day DATE,
    commands TEXT,
    id_pet INT,
    FOREIGN KEY (id_pet) REFERENCES Pets(id_pet)
);

DROP TABLE IF EXISTS Horses;
CREATE TABLE Horses (
    id_horse INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255),
    birth_day DATE,
    commands TEXT,
    id_pack_animal INT,
    FOREIGN KEY (id_pack_animal) REFERENCES PackAnimals(id_pack_animal)
);

DROP TABLE IF EXISTS Camels;
CREATE TABLE Camels (
    id_camel INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255),
    birth_day DATE,
    commands TEXT,
    id_pack_animal INT,
    FOREIGN KEY (id_pack_animal) REFERENCES PackAnimals(id_pack_animal)
);

DROP TABLE IF EXISTS Donkeys;
CREATE TABLE Donkeys (
    id_donkey INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255),
    birth_day DATE,
    commands TEXT,
    id_pack_animal INT,
    FOREIGN KEY (id_pack_animal) REFERENCES PackAnimals(id_pack_animal)
);
</pre>
# Задание №9
### Заполнить низкоуровневые таблицы именами(животных), командами которые они выполняют и датами рождения
<pre>
INSERT INTO HumanFriends (type_human_friend) VALUES ('Pet'), ('PackAnimal');
INSERT INTO Pets (type_pet, id_human_friend) VALUES ('Cat', 1), ('Dog', 1), ('Hamster', 1);
INSERT INTO PackAnimals (type_pack_animal, id_human_friend) VALUES ('Horse', 2), ('Camel', 2), ('Donkey', 2);
INSERT INTO Cats (name, birth_day, commands, id_pet) VALUES ('Whiskers', '2022-01-01', 'sit, jump', 1);
INSERT INTO Dogs (name, birth_day, commands, id_pet) VALUES ('Rex', '2021-05-10', 'fetch, sit', 2);
INSERT INTO Hamsters (name, birth_day, commands, id_pet) VALUES ('Nibbles', '2023-03-20', 'run', 3);
INSERT INTO Horses (name, birth_day, commands, id_pack_animal) VALUES ('Thunder', '2019-07-15', 'run', 1);
INSERT INTO Camels (name, birth_day, commands, id_pack_animal) VALUES ('Sandy', '2020-10-30', 'carry', 2);
INSERT INTO Donkeys (name, birth_day, commands, id_pack_animal) VALUES ('Eeyore', '2022-02-14', 'carry', 3);

SELECT * FROM HumanFriends;
SELECT * FROM Pets;
SELECT * FROM PackAnimals;
SELECT * FROM Cats;
SELECT * FROM Dogs;
SELECT * FROM Hamsters;
SELECT * FROM Horses;
SELECT * FROM Camels;
SELECT * FROM Donkeys;
</pre>
# Задание №10
### Удалив из таблицы верблюдов, т.к. верблюдов решили перевезти в другой питомник на зимовку. Объединить таблицы лошади, и ослы в одну таблицу.
<pre>
DELETE FROM Camels;
SELECT * FROM Camels;

DROP TABLE IF EXISTS HorsesAndDonkeys;
CREATE TABLE HorsesAndDonkeys AS
SELECT id_horse AS id, name, birth_day, commands, 'Horse' AS type FROM Horses
UNION
SELECT id_donkey AS id, name, birth_day, commands, 'Donkey' AS type FROM Donkeys;
</pre>
# Задание №11
### Создать новую таблицу “молодые животные” в которую попадут все животные старше 1 года, но младше 3 лет и в отдельном столбце с точностью до месяца подсчитать возраст животных в новой таблице
<pre>
DROP TABLE IF EXISTS YoungAnimals;
CREATE TABLE YoungAnimals AS
SELECT id, name, birth_day, commands, type,
       TIMESTAMPDIFF(MONTH, birth_day, CURDATE()) AS age_in_months
FROM (
    SELECT id_cat AS id, name, birth_day, commands, 'Cat' AS type FROM Cats
    UNION ALL
    SELECT id_dog AS id, name, birth_day, commands, 'Dog' AS type FROM Dogs
    UNION ALL
    SELECT id_hamster AS id, name, birth_day, commands, 'Hamster' AS type FROM Hamsters
    UNION ALL
    SELECT id AS id, name, birth_day, commands, type FROM HorsesAndDonkeys
) AS AllAnimals
WHERE TIMESTAMPDIFF(MONTH, birth_day, CURDATE()) BETWEEN 12 AND 36;
</pre>
# Задание №12
### Объединить все таблицы в одну, при этом сохраняя поля, указывающие на прошлую принадлежность к старым таблицам.
<pre>
DROP TABLE IF EXISTS AllAnimals;
CREATE TABLE AllAnimals AS
SELECT id_cat AS id, name, birth_day, commands, 'Cat' AS type FROM Cats
UNION
SELECT id_dog AS id, name, birth_day, commands, 'Dog' AS type FROM Dogs
UNION
SELECT id_hamster AS id, name, birth_day, commands, 'Hamster' AS type FROM Hamsters
UNION
SELECT id AS id, name, birth_day, commands, type FROM HorsesAndDonkeys
UNION
SELECT id AS id, name, birth_day, commands, type FROM YoungAnimals;
</pre>
