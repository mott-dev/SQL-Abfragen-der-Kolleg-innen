# SQL-Abfragen-der-Kolleg-innen

## 1:
SELECT Categories.CategoryID, Categories.CategoryName, OrderDetails.ProductID, Products.ProductName, Orders.OrderID, Orders.OrderDate FROM Orders INNER JOIN OrderDetails ON OrderDetails.OrderID = Orders.OrderID INNER JOIN Products ON Products.ProductID = OrderDetails.ProductID INNER JOIN Categories ON Categories.CategoryID = Products.CategoryID ORDER BY Categories.CategoryID ASC, Orders.OrderDate DESC

## 2:
SELECT * FROM Suppliers, OrderDetails, Orders, Products WHERE Orderdetails.OrderID = Orders.OrderID AND OrderDetails.ProductID = Products.ProductID AND Products.SupplierID = Suppliers.SupplierID AND Orders.OrderDate BETWEEN '1996-04-07' AND '1996-12-05' AND Orders.CustomerID = 8

## 3:


## 7:
SELECT * FROM Customers,Orders,OrderDetails where Customers.CustomerID= Orders.CustomerID and Orders.OrderID=OrderDetails.OrderID and Quantity>50 order by Quantity desc

## 8:
SELECT Products.ProductID, Products.ProductName, Products.SupplierID, Suppliers.SupplierName, Suppliers.ContactName FROM Products INNER JOIN Suppliers ON Products.SupplierID = Suppliers.SupplierID WHERE Suppliers.SupplierName < 'H%' AND Suppliers.ContactName = 'Cheryl Saylor' OR Suppliers.ContactName = 'Chantal Goulet';

## 9:
SELECT FirstName AS Vorname, COUNT(Orders.OrderID) AS AnzahlBestellungen FROM Employees LEFT JOIN Orders ON Employees.EmployeeID = Orders.EmployeeID GROUP BY FirstName

## 10:
SELECT Distinct o.OrderID, Sum(p.price * oD.quantity)  from Orders o, OrderDetails oD, Products p where oD.OrderID = o.OrderID AND p.ProductID = oD.ProductID Group by o.OrderID Having Sum(p.price * oD.quantity) > 2000

## 12:
SELECT Products.ProductID, Products.ProductName, Suppliers.SupplierID, Suppliers.SupplierName, Suppliers.ContactName FROM Products INNER JOIN Suppliers ON Products.SupplierID=Suppliers.SupplierID WHERE (Suppliers.SupplierName > 'A%' AND Suppliers.SupplierName < 'F%') AND (Suppliers.ContactName = "Charlotte Cooper" OR Suppliers.ContactName = "Cheryl Saylor") ORDER BY ProductName ASC;

## 13:
SELECT ord.OrderID,ord.OrderDate,pro.ProductName,pro.Price,odt.Quantity FROM Orders ord JOIN OrderDetails odt ON ord.OrderID = odt.OrderID JOIN Products pro ON odt.ProductID = pro.ProductID WHERE odt.Quantity > 30 ORDER BY pro.ProductName;

## 14:
Select * from (SELECT * FROM Orders o left join OrderDetails od ON o.OrderID = od.OrderID ORDER BY o.OrderID, Quantity DESC) o GROUP BY o.OrderID

## 15:
SELECT OrderID, CustomerID, EmployeeID, MAX(OrderDate), ShipperID FROM Orders
