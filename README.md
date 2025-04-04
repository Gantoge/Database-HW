# Проект "Базы данных"

Проект представляет собой создание, наполнение и выборку данных в БД MySQL.
Цель проекта - совершенствование знаний и навыков по предмету БД.

В проекте представлены 4 различные базы данных:
- транспортные средства;
- автомобильные гонки;
- бронирование отелей;
- структура организации.

Каждая из баз данных включает в себя этапы создания таблиц, наполнения их данными, а также решение задач. 
Каждая из представленных баз данных сопровождается скриптом, который создает таблицы базы данных и заполняет их тестовыми данными. 

## База данных 1. Транспортные средства.


Структура базы данных включает три таблицы для хранения информации о различных типах транспортных средств: 
Vehicle, Car, Motorcycle и Bicycle. 

#### 1. Таблица `Vehicle`
Содержит общую информацию о производителях и моделях транспортных средств.
 Поля:
    - `maker`: (VARCHAR) Название производителя автомобиля или мотоцикла.
    - `model`: (VARCHAR) Название модели. Это поле также служит первичным ключом, что означает, что каждая модель должна быть уникальной.
    - `type`: (ENUM) Тип транспортного средства, который может принимать одно из значений: 'Car', 'Motorcycle', 'Bicycle'.

#### 2. Таблица `Car`
Содержит детали о легковых автомобилях.
 Поля:
    - `vin`: (VARCHAR) Уникальный идентификатор автомобиля (номер VIN), который является первичным ключом.
    - `model`: (VARCHAR) Название модели автомобиля, которая ссылается на поле `model` в таблице `Vehicle`. Это поле используется как внешний ключ для обеспечения целостности данных.
    - `engine_capacity`: (DECIMAL) Объем двигателя в литрах.
    - `horsepower`: (INT) Мощность двигателя в лошадиных силах.
    - `price`: (DECIMAL) Цена автомобиля в долларах.
    - `transmission`: (ENUM) Тип трансмиссии, которая может быть 'Automatic' (автоматическая) или 'Manual' (механическая).

#### 3. Таблица `Motorcycle`
Содержит детали о мотоциклах.
 Поля:
    - `vin`: (VARCHAR) Уникальный идентификатор мотоцикла (номер VIN), который является первичным ключом.
    - `model`: (VARCHAR) Название модели мотоцикла, которая ссылается на поле `model` в таблице `Vehicle`, используется как внешний ключ.
    - `engine_capacity`: (DECIMAL) Объем двигателя в литрах.
    - `horsepower`: (INT) Мощность двигателя в лошадиных силах.
    - `price`: (DECIMAL) Цена мотоцикла в долларах.
    - `type`: (ENUM) Тип мотоцикла, который может принимать одно из значений: 'Sport', 'Cruiser', 'Touring'.

#### 4. Таблица `Bicycle`
Содержит детали о велосипедах.
 Поля:
    - `serial_number`: (VARCHAR) Уникальный серийный номер велосипеда, который является первичным ключом.
    - `model`: (VARCHAR) Название модели велосипеда, которая ссылается на поле `model` в таблице `Vehicle`, используется как внешний ключ.
    - `gear_count`: (INT) Количество передач велосипеда.
    - `price`: (DECIMAL) Цена велосипеда в долларах.
    - `type`: (ENUM) Тип велосипеда, который может принимать одно из значений: 'Mountain', 'Road', 'Hybrid'.

#### Взаимосвязи
- Каждая из таблиц `Car`, `Motorcycle` и `Bicycle` ссылается на таблицу `Vehicle` через поле `model`, что обеспечивает целостность данных. Это значит, что каждая модель, указанная в таблицах `Car`, `Motorcycle` и `Bicycle`, должна предварительно существовать в таблице `Vehicle`.
- Таблицы `Car`, `Motorcycle` и `Bicycle` можно считать подмножествами таблицы `Vehicle`, где каждая подтаблица содержит специфические детали для каждого типа транспортного средства.

Данная структура базы данных организует информацию о транспортных средствах в соответствии с их типами и основными характеристиками. Она позволяет удобно хранить, просматривать и поддерживать данные о различных моделях автомобилей, мотоциклов и велосипедов, сохраняя при этом их связь с производителями.

### Подготовительный этап:
1. Создадим БД vehicles в графическом интерфейсе.
2. Создадим таблицы, запустив скрипт из файла databases/vehicles/create_tables.sql.
3. Наполним таблицы данными с помощью скрипта databases/vehicles/insert_data.sql.

### Задачи:
#### Задача 1.
Условие:
Найдите производителей (maker) и модели всех мотоциклов, которые имеют мощность более 150 лошадиных сил, 
стоят менее 20 тысяч долларов и являются спортивными (тип Sport). Также отсортируйте результаты 
по мощности в порядке убывания.

Решение:
размещено в скрипте databases/vehicles/task1.sql.

#### Задача 2.

Решение:
размещено в скрипте databases/vehicles/task2.sql.


## База данных 2. Автомобильные гонки.

### Условие
Структура базы данных включает в себя четыре основные таблицы, которые организуют информацию о классе автомобилей, самих автомобилях, гонках и результатах гонок. Рассмотрим каждую из таблиц детальнее:

#### 1. Таблица `Classes`
 Хранит информацию о различных классах автомобилей.
 Поля:
    - `class`: (VARCHAR) Название класса автомобилей, который служит первичным ключом и должен быть уникальным для каждого класса.
    - `type`: (ENUM) Тип класса, который может принимать значения 'Racing' или 'Street', определяющие назначения автомобилей.
    - `country`: (VARCHAR) Страна, с которой связан этот класс автомобилей.
    - `numDoors`: (INT) Количество дверей в автомобиле данного класса.
    - `engineSize`: (DECIMAL) Размер двигателя в литрах, с точностью до одного знака после запятой.
    - `weight`: (INT) Вес автомобиля в килограммах.

#### 2. Таблица `Cars`
Хранит информацию об автомобилях.
 Поля:
    - `name`: (VARCHAR) Название автомобиля, которое служит первичным ключом и должно быть уникальным.
    - `class`: (VARCHAR) Название класса, к которому принадлежит автомобиль. Это поле используется как внешний ключ, ссылающийся на поле `class` в таблице `Classes`. Это обеспечивает целостность данных, гарантируя, что каждый автомобиль относится к существующему классу.

#### 3. Таблица `Races`
 Хранит информацию о гонках.
 Поля:
    - `name`: (VARCHAR) Название гонки, которое служит первичным ключом и должно быть уникальным.
    - `date`: (DATE) Дата проведения гонки, что позволяет сохранить информацию о времени гонки.

#### 4. Таблица `Results`
 Хранит результаты гонок для автомобилей.
 Поля:
    - `car`: (VARCHAR) Название автомобиля, который участвовал в гонке. Это поле используется как внешний ключ, ссылающийся на поле `name` в таблице `Cars`.
    - `race`: (VARCHAR) Название гонки, в которой участвовал автомобиль. Это поле используется как внешний ключ, ссылающийся на поле `name` в таблице `Races`.
    - `position`: (INT) Позиция, которую автомобиль занял в гонке. Это число указывает на успешность участия автомобиля в конкретной гонке.
    - Пара (car, race) образует первичный ключ, гарантируя уникальность каждой записи в таблице результатов, так как один автомобиль не может участвовать в одной гонке более одного раза.

#### Взаимосвязи
- Таблица `Cars` ссылается на таблицу `Classes`, обеспечивая связку между автомобилями и их классами.
- Таблица `Results` связывает автомобили с гонками, предоставляя информацию о том, какое место занял каждый автомобиль в конкретной гонке. Ссылки на таблицы `Cars` и `Races` обеспечивают целостность и согласованность данных.

Данная структура базы данных организует и систематизирует информацию о классах автомобилей, самих автомобилях, гонках и их результатах. Она позволяет удобно хранить и обрабатывать данные о гоночных классах, автомобилях и их участии в гонках, сохраняя при этом целостность и связь между записями.

### Подготовительный этап:
1. Создадим БД car_races в графическом интерфейсе.
2. Создадим таблицы, запустив скрипт из файла databases/car_races/create_tables.sql.
3. Наполним таблицы данными с помощью скрипта databases/car_races/insert_data.sql.

### Задачи:
#### Задача 1.

Решение:
размещено в скрипте databases/car_races/task1.sql.

#### Задача 2.

Решение:
размещено в скрипте databases/car_races/task2.sql.

#### Задача 3.
Решение:
размещено в скрипте databases/car_races/task3.sql.

#### Задача 4.
Решение:
размещено в скрипте databases/car_races/task4.sql.

#### Задача 5.
Решение:
размещено в скрипте databases/car_races/task5.sql.

## База данных 3. Бронирование отелей.

#### 1. Таблица `Hotel`
 Хранит информацию о гостиницах.
 Поля:
    - `ID_hotel`: (INT) Уникальный идентификатор гостиницы, который служит первичным ключом. Этот идентификатор должен быть уникальным для каждой записи в таблице.
    - `name`: (VARCHAR) Название гостиницы. Это обязательное поле, которое не может быть пустым.
    - `location`: (VARCHAR) Местоположение гостиницы. Это также обязательное поле, не допускающее пустых значений.

#### 2. Таблица `Room`
 Хранит информацию о номерах в гостиницах.
 Поля:
    - `ID_room`: (INT) Уникальный идентификатор номера, который служит первичным ключом и должен быть уникальным для каждого номера.
    - `ID_hotel`: (INT) Идентификатор гостиницы, к которой принадлежит номер. Это поле используется как внешний ключ, ссылающийся на `ID_hotel` в таблице `Hotel`, что обеспечивает связь между номерами и гостиницами.
    - `room_type`: (ENUM) Тип номера, который может принимать значения 'Single', 'Double' или 'Suite', указывая на тип размещения.
    - `price`: (DECIMAL) Цена номера за ночь, представлена с точностью до двух знаков после запятой.
    - `capacity`: (INT) Вместимость номера, то есть максимальное количество людей, которые могут разместиться в данном номере.

#### 3. Таблица `Customer`
 Хранит информацию о клиентах гостиницы.
 Поля:
    - `ID_customer`: (INT) Уникальный идентификатор клиента, который служит первичным ключом. Этот идентификатор должен быть уникальным.
    - `name`: (VARCHAR) Имя клиента. Это обязательное поле, которое не может быть пустым.
    - `email`: (VARCHAR) Электронная почта клиента. Это обязательное поле, и его значения должны быть уникальными, чтобы избежать дубликатов. Оно не может быть пустым.
    - `phone`: (VARCHAR) Номер телефона клиента. Это обязательное поле, не допускающее пустых значений.

#### 4. Таблица `Booking`
 Хранит информацию о бронированиях.
 Поля:
    - `ID_booking`: (INT) Уникальный идентификатор бронирования, который служит первичным ключом.
    - `ID_room`: (INT) Идентификатор номера, который забронирован. Это поле используется как внешний ключ, ссылающийся на `ID_room` в таблице `Room`, что обеспечивает связь между бронированиями и номерами.
    - `ID_customer`: (INT) Идентификатор клиента, который сделал бронирование. Это поле используется как внешний ключ, ссылающийся на `ID_customer` в таблице `Customer`, которым мы обеспечиваем связь между бронированиями и клиентами.
    - `check_in_date`: (DATE) Дата заезда, указывающая, когда клиент планирует заехать в номер. Это обязательное поле.
    - `check_out_date`: (DATE) Дата выезда, указывающая, когда клиент планирует покинуть номер. Это обязательное поле.

#### Взаимосвязи
- Таблица `Room` ссылается на таблицу `Hotel`, обеспечивая связь между номерами и соответствующими гостиницами.
- Таблица `Booking` связывает номера и клиентов, обеспечивая информацию о том, какие номера были забронированы конкретными клиентами.
- Использование внешних ключей (в `Room` и `Booking`) поддерживает целостность данных, гарантируя, что все ссылки на гостиницы, номера и клиентов верны.

Данная структура базы данных эффективно организует и систематизирует информацию о гостиницах, номерах, клиентах и их бронированиях. Это позволяет удобно управлять данными, обеспечивая целостность информации и легкость доступа к различным аспектам гостиничного сервиса.

### Подготовительный этап:
1. Создадим БД hotels_booking в графическом интерфейсе.
2. Создадим таблицы, запустив скрипт из файла databases/hotels_booking/create_tables.sql.
3. Наполним таблицы данными с помощью скрипта databases/hotels_booking/insert_data.sql.

### Задачи:
#### Задача 1.
Решение:
размещено в скрипте databases/hotels_booking/task1.sql.

#### Задача 2.
Условие:
Решение:
размещено в скрипте databases/hotels_booking/task2.sql.

#### Задача 3.
Решение:
размещено в скрипте databases/hotels_booking/task3.sql.

## База данных 4. Структура организации.

### Условие.
Структура базы данных предназначена для управления информацией о сотрудниках, их ролях, департаментах, проектах и задачах. Она состоит из пяти таблиц: `Departments`, `Roles`, `Employees`, `Projects` и `Tasks`. Рассмотрим каждую таблицу подробнее.

#### 1. Таблица `Departments`
 Хранит информацию о департаментах в организации.
 Поля:
    - `DepartmentID`: (INT) Уникальный идентификатор департамента, который является первичным ключом. Этот идентификатор должен быть уникальным для каждой записи.
    - `DepartmentName`: (VARCHAR) Название департамента. Это обязательное поле (NOT NULL), которое не может быть пустым.

#### 2. Таблица `Roles`
 Хранит информацию о ролях сотрудников внутри организации.
 Поля:
    - `RoleID`: (INT) Уникальный идентификатор роли, который служит первичным ключом. Этот идентификатор должен быть уникальным.
    - `RoleName`: (VARCHAR) Название роли. Это также обязательное поле (NOT NULL), не допускающее пустых значений.

#### 3. Таблица `Employees`
 Хранит информацию о сотрудниках организации.
 Поля:
    - `EmployeeID`: (INT) Уникальный идентификатор сотрудника, который является первичным ключом. Этот идентификатор должен быть уникальным для каждого сотрудника.
    - `Name`: (VARCHAR) Имя сотрудника. Это обязательное поле (NOT NULL), которое не может быть пустым.
    - `Position`: (VARCHAR) Должность сотрудника. Это поле может быть пустым.
    - `ManagerID`: (INT) Идентификатор менеджера, который также является сотрудником. Это поле используется как внешний ключ, ссылающийся на `EmployeeID` в той же таблице `Employees`, что позволяет создать иерархию менеджеров и подчиненных.
    - `DepartmentID`: (INT) Идентификатор департамента, к которому принадлежит сотрудник. Это поле используется как внешний ключ, ссылающийся на `DepartmentID` в таблице `Departments`.
    - `RoleID`: (INT) Идентификатор роли, которая соответствует сотруднику. Это поле используется как внешний ключ, ссылающийся на `RoleID` в таблице `Roles`.

#### 4. Таблица `Projects`
 Хранит информацию о проектах организованными отделами.
 Поля:
    - `ProjectID`: (INT) Уникальный идентификатор проекта, который является первичным ключом. Этот идентификатор должен быть уникальным для каждого проекта.
    - `ProjectName`: (VARCHAR) Название проекта. Это обязательное поле (NOT NULL), не допускающее пустых значений.
    - `StartDate`: (DATE) Дата начала проекта. Это поле может быть пустым.
    - `EndDate`: (DATE) Дата окончания проекта. Это поле может быть пустым.
    - `DepartmentID`: (INT) Идентификатор департамента, который отвечает за проект. Это поле используется как внешний ключ, ссылающийся на `DepartmentID` в таблице `Departments`.

#### 5. Таблица `Tasks`
 Хранит информацию о задачах, назначенных на сотрудников в рамках проектов.
 Поля:
    - `TaskID`: (INT) Уникальный идентификатор задачи, который служит первичным ключом. Этот идентификатор должен быть уникальным для каждой задачи.
    - `TaskName`: (VARCHAR) Название задачи. Это обязательное поле (NOT NULL), не допускающее пустых значений.
    - `AssignedTo`: (INT) Идентификатор сотрудника, которому назначена задача. Это поле используется как внешний ключ, ссылающийся на `EmployeeID` в таблице `Employees`.
    - `ProjectID`: (INT) Идентификатор проекта, к которому относится задача. Это поле используется как внешний ключ, ссылающийся на `ProjectID` в таблице `Projects`.

#### Взаимосвязи
- Таблицы `Employees`, `Projects`, и `Tasks` связаны между собой через внешние ключи, что позволяет интегрировать данные о сотрудниках, их задачах и проектах.
- `ManagerID` в `Employees` позволяет создать иерархическую структуру управления, связывая сотрудников с их менеджерами.
- `DepartmentID` связывает `Employees` с соответствующими департаментами, а также проекты с организацией в рамках определенного департамента.
- `RoleID` связывает сотрудников с их ролями, что позволяет классифицировать их функции внутри компании.

Данная структура базы данных обеспечивает четкое управление данными о департаментах, ролях сотрудников, их проектах и задачах. Это позволяет эффективно организовывать, отслеживать и управлять ресурсами и задачами в компании, что является ключевым для успешного функционирования и достижения бизнес-целей.

### Подготовительный этап:
1. Создадим БД company_structure в графическом интерфейсе.
2. Создадим таблицы, запустив скрипт из файла databases/company_structure/create_tables.sql.
3. Наполним таблицы данными с помощью скрипта databases/company_structure/insert_data.sql.

#### Задачи:
#### Задача 1.
Решение:
размещено в скрипте databases/company_structure/task1.sql.

#### Задача 2.
Решение:
размещено в скрипте databases/company_structure/task2.sql.

#### Задача 3.
Решение:
размещено в скрипте databases/company_structure/task3.sql.