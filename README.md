# SQL-Abfragen-der-Kolleg-innen


## 8:
SELECT Products.ProductID, Products.ProductName, Products.SupplierID, Suppliers.SupplierName, Suppliers.ContactName FROM Products INNER JOIN Suppliers ON Products.SupplierID = Suppliers.SupplierID WHERE Suppliers.SupplierName < 'H%' AND Suppliers.ContactName = 'Cheryl Saylor' OR Suppliers.ContactName = 'Chantal Goulet';

## 9:
SELECT FirstName AS Vorname, COUNT(Orders.OrderID) AS AnzahlBestellungen FROM Employees LEFT JOIN Orders ON Employees.EmployeeID = Orders.EmployeeID GROUP BY FirstName

## 10:
SELECT Distinct o.OrderID, Sum(p.price * oD.quantity)  from Orders o, OrderDetails oD, Products p where oD.OrderID = o.OrderID AND p.ProductID = oD.ProductID Group by o.OrderID Having Sum(p.price * oD.quantity) > 2000

## 14:
Select * from (SELECT * FROM Orders o left join OrderDetails od ON o.OrderID = od.OrderID ORDER BY o.OrderID, Quantity DESC) o GROUP BY o.OrderID
