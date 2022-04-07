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
3. GROUP BY
4. HAVING
5. SELECT
6. ORDER BY

#### Selecting data with sorting
Keywords: **ORDER BY, ASC, DESC**
_Example:_
SELECT _author_, _title_, _amount_ AS _Количество_
FROM _book_
WHERE _price_ < 750
ORDER BY _author_, _amount_ DESC;

#### Selecting data with operator LIKE
Keywords: **LIKE**
_Example:_
SELECT _title_
FROM _book_
WHERE _title_ LIKE _'Б%'_;

#### Selecting unique elements of a column
Keywords: **DISTINCT, GROUP BY**
_Example:_
SELECT DISTINTC _author_
FROM _book_;

SELECT _author_
FROM _book_
GROUP BY _author_;

#### Selecting data, group functions SUM and COUNT
Keywords: **COUNT, SUM**
_Example:_
SELECT _author_, COUNT(_author_), COUNT(_amount_), COUNT(*)
FROM _book_
GROUP BY _author_;

#### Selecting data, group functions MIN, MAX, AVG
Keywords: **MIN, MAX, AVG**
_Example:_
SELECT _author_, MIN(_price_) AS _min\_price_
FROM _book_
GROUP BY _author_;

#### Selecting data based on conditions, group functions
Keywords: **HAVING**
_Example:_
SELECT _author_
  MIN(_price_) AS _Minimal\_price_,
  MAX(_price_) AS _Maximum\_price_
FROM _book_
GROUP BY _author_
HAVING SUM(_price_ * _amount_) > _5000_;

#### Nested queries in WHERE clause
_Example_:
SELECT _title_, _author_, _price_, _amount_
FROM _book_
WHERE _price_ = (
  SELECT MIN(_price_)
  FROM _book_
);

#### Nested query, operator IN
_Example:_
SELECT _title_, _author_, _price_
FROM _book_
WHERE _author_ IN (
  SELECT _author_
  FROM _book_
  GROUP BY _author_
  HAVING SUM(_amount_) >= 12
);

#### Nested queries, operators ANY and ALL
_Example:_
SELECT _title_, _author_, _amount_, _price_
FROM _book_
WHERE _amount_ < ALL (
  SELECT AVG(_amount_)
  FROM _book_
  GROUP BY _author_
);
**NOTE**: ANY and ALL are used only with nested queries

#### Inserting entries from another table
_Example:_
INSERT INTO _book_(_title_, _author_, _price_, _amount_)
  SELECT _title_, _author_, _price_, _amount_
  FROM _supply_
  WHERE _author_ NOT IN ('_Булгаков М.А._', '_Достоевский Ф.М._');

#### Update query
Keywords: **UPDATE, SET**
_Example:_
UPDATE _book_
SET _price_ = 0.7 * _price_
WHERE _amount_ < 5;

#### Delete query
Keywords: **DELETE**
_Example:_
DELETE FROM _supply_
WHERE _title_ IN (
  SELECT _title_
  FROM _book_
);

#### Limiting the table output
Keyword: **LIMIT**
_Example:_
SELECT *
FROM _trip_
ORDER BY _date\_first_
LIMIT 1;

#### DATEDIFF function
_Example:_
DATEDIFF('2020-04-01', '2020-03-28')=4

#### MONTH function
_Example:_
MONTH('2020-04-12')=4

#### MONTHNAME function
_Example:_
MONTHNAME('2020-04-12')='April'

#### DAY, MONTH, YEAR functions
_Example:_
DAY('2020-02-01')=1
MONTH('2020-02-01')=2
YEAR('2020-02-01)=2020

#### Creating a table with foreign keys
Keywords: **FOREIGN KEY, REFERENCES**
_Example:_
CREATE TABLE _book_ (
    _book\_id_ INT PRIMARY KEY AUTO_INCREMENT, 
    _title_ VARCHAR(50), 
    _author\_id_ INT NOT NULL, 
    _price_ DECIMAL(8,2), 
    _amount_ INT, 
    FOREIGN KEY (_author\_id_)  REFERENCES author (_author\_id_) 
);

#### After deleting entry from main table
Keywords: **ON DELETE, CASCADE, SET NULL, SET DEFAULT, RESTRICT**
_Example:_
CREATE TABLE _book_ (
    _book\_id_ INT PRIMARY KEY AUTO_INCREMENT, 
    _title_ VARCHAR(50), 
    _author\_id_ INT NOT NULL, 
    _price_ DECIMAL(8,2), 
    _amount_ INT, 
    FOREIGN KEY (_author\_id_)  REFERENCES _author_ (_author\_id_) ON DELETE CASCADE
);

#### INNER JOIN
Keywords: **INNER JOIN, ON**
_Example:_
SELECT _title_, _name\_author_
FROM 
    _author_ INNER JOIN _book_
    ON _author.author\_id_ = _book.author\_id_;

#### LEFT and RIGHT OUTER JOIN
Keywords: ***LEFT JOIN, RIGHT JOIN***
_Example:_
SELECT _name\_author_, _title_ 
FROM _author_ LEFT JOIN _book_
     ON _author.author\_id_ = _book.author\_id_
ORDER BY _name\_author_;

#### CROSS JOIN
Keywords: **CROSS JOIN**
_Example:_
SELECT _name\_author_, _name\_genre_
FROM 
    _author_ CROSS JOIN _genre_;

#### RAND, DATE_ADD functions
Keywords: **RAND, DATE_ADD**
_Example_:
DATE_ADD('2020-02-02', INTERVAL 45 DAY) returns 18 March 2020
DATE_ADD('2020-02-02', INTERVAL 6 MONTH) returns 2 AUGUST 2020
FLOOR(RAND() * 365)

#### Joining tables with USING
Keywords: **USING**
_Example:_
SELECT _title_, _name\_author_, _author\_id_
FROM 
    _author_ INNER JOIN _book_
    USING(_author\_id_);
