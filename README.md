# Задача
В базе данных MS SQL Server есть продукты и категории. Одному продукту может соответствовать много категорий, в одной категории может быть много продуктов. Напишите SQL запрос для выбора всех пар «Имя продукта – Имя категории». Если у продукта нет категорий, то его имя все равно должно выводиться.

# Решения
```SQL
CREATE TABLE Products (
	Id INT  IDENTITY(1,1) NOT NULL,
	Name nvarchar(50),
	Primary Key(Id)
);
```

INSERT INTO Products
VALUES
	('Java'),
	('C#'),
	('Opel'),
	('KIA '),
	('Range Rower'),
	('Thosihiba');

CREATE TABLE Categories (
	Id INT  IDENTITY(1,1) NOT NULL,
	Name nvarchar(50),
	Primary Key(Id)
);

INSERT INTO Categories
VALUES
	('Book'),
	('Car'),
	('Computer');

CREATE TABLE ProductCategories (
    Id INT  IDENTITY(1,1) NOT NULL,
	ProductId INT FOREIGN KEY REFERENCES Products(Id),
	CategoryId INT FOREIGN KEY REFERENCES Categories(Id),
	Primary Key(Id)
);

INSERT INTO ProductCategories
VALUES
	(1, 1),
	(2, 1),
	(3, 2),
	(4,2),
	(5,2),
	(6,3);

SELECT P.Name, C.Name
FROM Products P
LEFT JOIN ProductCategories PC
	ON P.Id = PC.ProductId
LEFT JOIN Categories C
	ON PC.CategoryId = C.Id;
