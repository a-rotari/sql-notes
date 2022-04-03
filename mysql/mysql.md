#### Show all databases
SHOW DATABASES;

#### Select a database
USE database_name;

#### Describe a table
DESCRIBE [table_name];

#### Create a table
Keywords: **CREATE TABLE**

_Example:_
CREATE TABLE _genre_(
  _genre\_id_ INT PRIMARY KEY AUTO_INCREMENT,
  _name\_genre_ VARCHAR(30)
);

#### Insert an entry into the table
Keywords: **INSERT INTO, VALUES**
_Example:_
INSERT INTO _table_(_field1_, _field2_)
VALUES (_value1_, _value2_);

#### Show the entire table
Keywords: **SELECT, FROM**
_Example:_
SELECT * FROM _genre_;
SELECT _title_, _amount_ FROM _book_;

#### Selecting new columns and assigning new names
Keywords: **SELECT, AS, FROM**
_Example:_
SELECT _title_ AS _assigned\_name_, _amount_
FROM _book_;

#### Selecting data using a computed column
_Example_:
SELECT  _title_, _author_, _price_, _amount_,
        _price * amount_ AS _total_
FROM _book_;

#### Selecting data, computed columns, mathematical functions
Functions: **CEILING(x), ROUND(x, k), FLOOR(x), POWER(x, y), SQRT(x),**
           **DEGREES(x), RADIANS(x), ABS(x), PI()**

#### Selecting data, computed tables, logic functions
Functions: **IF**
_Example:_
SELECT _title_, _amount_, _price_, 
    IF(_amount_<4, price\*0.5, price\*0.7) AS _sale_
    FROM _book_; 

#### Selecting data based on conditional
Keyword: **WHERE**
_Example_:
SELECT _title_, _price_
FROM _book_
WHERE _price_ < 600;

##### Priority of operations
1. brackets
2. multiplication (*), division (/)
3. addition (+), subtraction (-)
4. comparison operators (=, >, <, >=, <=, <>)
5. NOT
6. AND
7. OR

#### Selecting data, BETWEEN, IN
Keywords: **BETWEEN**, **IN**
_Example:_ 
SELECT _title_, _amount_
FROM _book_
WHERE _amount_ BETWEEN 5 AND 14;

SELECT _title_, _price_
FROM _book_
WHERE _author_ IN ('Булгаков М.А', 'Достоевский Ф.М.');

#### Logical sequence of operations
1. FROM
2. WHERE
3. SELECT
4. ORDER BY

#### Selecting data with sorting
Keywords: **ORDER BY, ASC, DESC**
_Example:_
SELECT _author_, _title_, _amount_ AS _Количество_
FROM _book_
WHERE _price_ < 750
ORDER BY _author_, _amount_ DESC;
