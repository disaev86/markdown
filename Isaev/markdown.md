# 1. ФИО, группа
 
  Исаев Динислам Абдулмуталимович, ИС 22/9-1

# 2. Описание БД

Моя база данных про зоопарк
База данных имеет 5 таблиц

Таблица Animals (таблица хранит сведения о животных)

Таблица Employees (таблица хранит сведения о сотрудниках)

Таблица Feeding (таблица хранит сведения о корме животных)

Таблица Medical_examination (таблица хранит сведения роста, веста и о прививках животных)

Таблица Room (таблица хранит сведения о вольерах животных)

## 2.1

###### Таблица Animals состоит из следущих атрибутов:
* id - создается по умолчанию, INT
* id_feeding - айди к таблице Feeding, INT
* id_room - айди к таблице Room, INT
* id_examination - айди к таблице Medical_examination, INT
* name_animal - название животного, VARCHAR(30)
* type_of_animal - тип животного, VARCHAR(30)

![](screens/Animals1.png)

![](screens/Animals2.png)


###### Таблица Employees состоит из следущих атрибутов:
* id - создается по умолчанию, INT
* post - должность сотрудника, VARCHAR(30)

![](screens/Employees2.png)
![](screens/Employees1.png)


###### Таблица Feeding состоит из следущих атрибутов:
* id - создается по умолчанию, INT
* feeding_time - время кормления животных, TIME
* type_of_feed - тип корма, VARCHAR(30)

![](screens/feeding1.png)
![](screens/feeding2.png)


###### Таблица Medical_examination из следущих атрибутов:
* id - создается по умолчанию, INT
* weight - вес животного, DECIMAL(6,2)
* height - рост животного, DECIMAL(6,2)
* vaccations - имеются ли прививки у животного, VARCHAR(30)

![](screens/medical1.png)
![](screens/medical2.png)

###### Таблица Room состоит из следущих атрибутов:
* id - создается по умолчанию, INT
* id_employees - айди к таблице Employees

![](screens/room1.png)
![](screens/room2.png)	


# 3. Демонстрация работы функции UNION

Объединения двух наборов строк
Я объединил name_animal из таблицы Animals с type_of_animal с той же таблицы

```
SELECT name_animal AS Название_и_тип_животного
FROM Animals

UNION

SELECT type_of_animal AS Название_и_тип_животного
FROM Animals
```

### Результат:
![](screens/union.png)

Вывелся один запрос, состоящий из двух запросов


# 4. Демонстрация работы функции ORDER BY

Сортировка полученных строк
Я отсортировал вес животных

### По возрастанию:

```
SELECT
	name_animal,
	weight
FROM Animals
JOIN Medical_examination
	ON Animals.id_examination = Medical_examination.id
ORDER BY weight
```
![](screens/orderby1.png)

Вывелась таблица, отсортированная по возрастанию веса


### По убыванию:

```
SELECT
	name_animal,
	weight
FROM Animals
JOIN Medical_examination
	ON Animals.id_examination = Medical_examination.id
ORDER BY weight DESC
```

![](screens/orderby2.png)

Вывелась таблица, отсортированная по убыванию веса


### По алфавиту:

```
SELECT
	name_animal,
	weight
FROM Animals
JOIN Medical_examination
	ON Animals.id_examination = Medical_examination.id
ORDER BY name_animal
```

![](screens/orderby3.png)

Вывелась таблица, отсортированная по возрастанию алфавита

### В обратном алфавитном порядке:

```
SELECT
	name_animal,
	weight
FROM Animals
JOIN Medical_examination
	ON Animals.id_examination = Medical_examination.id
ORDER BY name_animal DESC
```

![](screens/orderby4.png)

Вывелась таблица, отсортированная в обратном порядке алфавита


# 5. Демонстрация работы функции HAVING

Получение данных из таблицы базы, соответствующих определённым значениям результатов
Я вывел имя животных у которых вес больше 200 кг

```
SELECT
	name_animal,
	weight
FROM Animals
JOIN Medical_examination
	ON Animals.id_examination = Medical_examination.id
GROUP BY name_animal
HAVING weight > 200
```

![](screens/having.png)

Вывелась таблица с животными, у которых вес больше двухсот килограмм


# 6. Демонстрация работы вложенных запросов

## 6.1 В SELECT

Хочу вывести количество привитых животных и имя животных в одном запросе
Для этого будем использовать вложенный запрос внутри SELECT

```
SELECT 
	name_animal, 
        (SELECT COUNT(*) FROM Medical_examination WHERE vaccinations LIKE 'yes') AS количество_привитых_животных
FROM Animals 
JOIN Medical_examination
	ON Animals.id_examination = Medical_examination.id
```

![](screens/attached_request.png)

Вывелась таблица с количеством привитых животных с помощью вложенного запроса

## 6.2 В WHERE

Хочу вывести имя животного с минимальным ростом
Для этого будем использовать вложенный запрос внутри WHERE

```
SELECT 
	name_animal,
    height
FROM Animals
JOIN Medical_examination
	ON Animals.id_examination = Medical_examination.id
WHERE height LIKE (SELECT MIN(height) FROM Medical_examination)
```

![](screens/attached_request2.png)

Вывелась таблица с именем животного, имеющий минимальный рост


# 7. Демонстрация работы оконных функций

# 7.1 Агрегатные функции

Хочу вывести минимальный вес



	
		
	
  
