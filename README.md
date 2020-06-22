# SQL-Abfragen-der-Kolleg-innen

## SQL W3Schools Übungsaufgaben
[https://www.w3schools.com/sql/trysql.asp?filename=trysql_select_all](https://www.w3schools.com/sql/trysql.asp?filename=trysql_select_all)



## Aufgaben
### 1:
Selektieren Sie: CategoryID, CategoryName, ProductID, ProductName, OrderID, OrderDate der Tabellen Categories, OrderDetails und Orders, wenn ProductID größer als 2 und CategoryID kleiner als 8, sortiert nach CategoryID aufsteigend, dann nach OrderDate absteigend
### 2:
Ein Kunde beschwert sich ständig über die Qualität der gelieferten Produkte. Gib alle LieferantenIDs (Supplier) und LieferantenNamen aus, die im Zeitraum vom 7/4/1996 bis zum 12/5/1996 bei Aufträgen vom Kunden mit der KundenNr. 8 beteilgt waren.
### 3:
Die Qualität des Produkts “ Chef Anton's Gumbo Mix“  lässt nach. Gib alle Lieferantennamen, die das Produkt „Chef Anton's Gumbo Mix“ liefern, gruppiert nach Land aus.
### 4:
In dem Produkt „Gustaf's Knäckebröd „ wurden gefährliche Viren entdeckt! Liefere alle KundenIDs und Kundennamen, welche im Zeitraum vom 12/12/1996 bis zum 2/11/1997 das Produkt „Gustaf's Knäckebröd“ bestellt haben
### 5:
Produktname und LieferantenIDs aller Lieferanten, welche Produkte liefern, deren Unit unter 5 liegt, aufteigend geordnet.
### 6:
Rufen Sie alle Bestellungen im Zeitraum vom 1996-08-02 bis 1997-01-30 ab und zeigen Sie alle Bestellungen an, die vom Lieferanten "United Package" und "Federal Shipping" ausgeliefert werden und ein Produkt von allen Hersteller/Zulieferer(Supplier) außer ID 16 & 18. Zeigen Sie dazu in jeder Row die dazugehörigen Kunden(Customers), Mitarbeiter(Employees) sowie Lieferantendaten(Shippers) an.
### 7:
Liste von Kunden Details und ihren Bestellungen Details und der menge ist große als 50 stück und sortieren sie den liste nach Menge absteigend??
### 8:
Wie 13, nur dass alle Supplier ausgegeben werden sollen, deren Anfangsbuchstabe im SupplierName von A-G ist und der ContactName "Cheryl Saylor" oder "Chantal Goulet" ist
### 9:
Selektieren Sie die Anzahl der Bestellungen als AnzahlBestellungen die einem Mitarbeiter zugeordnet sind, zusammen mit dem Namen des Mitarbeiters.
### 10:
Gebe alle OrderIDs und Gesamtbestellwert von Bestellungen aus, die einen Gesamtbestellwert von 2000€ überschreiten
### 11:
Erstellen sie eine Abfrage die Folgendes ausgibt (Auch die Spaltennamen bitte dementsprechend anpassen): KundenID, AngestelltenID, Produkt Name, LieferantenID, Menge und alle Spalten der Suppliers Tabelle aus den Tabellen Orders, OrderDetails, Products, Suppliers, bei denen die LieferantenID größer als 5, jedoch kleiner als 10 ist. Ordnen Sie das Ergebnis aufsteigend nach der KundenID und dem Produktnamen.
### 12:
Wie 13, nur dass alle Supplier ausgegeben werden sollen, deren Anfangsbuchstabe vom SupplierName im Bereich von A-F liegt und der ContactName "Charlotte Cooper" oder "Cheryl Saylor" ist.
### 13:
Fassen Sie eine Übersicht von OrderID, OrderDate, ProductName, Preis und Anzahl sortiert nach dem ProductName zusammen, wenn mehr als 30 Teile eines Produktes bestellt wurden. Hierzu sollen moderne Methoden verwendet werden.
### 14:
Alle Orders und die zugehörigen OrderDetails, wobei nur die Order mit der höchsten Quantity der jeweiligen ID angezeigt wird

### 15:
Selektieren Sie ausschließlich den letzten Datensatz (größtest „OrderDate“) der Tabelle „Orders“.



## Lösungen
### 1:
SELECT Categories.CategoryID, Categories.CategoryName, OrderDetails.ProductID, Products.ProductName, Orders.OrderID, Orders.OrderDate FROM Orders INNER JOIN OrderDetails ON OrderDetails.OrderID = Orders.OrderID INNER JOIN Products ON Products.ProductID = OrderDetails.ProductID INNER JOIN Categories ON Categories.CategoryID = Products.CategoryID ORDER BY Categories.CategoryID ASC, Orders.OrderDate DESC

### 2:
SELECT * FROM Suppliers, OrderDetails, Orders, Products WHERE Orderdetails.OrderID = Orders.OrderID AND OrderDetails.ProductID = Products.ProductID AND Products.SupplierID = Suppliers.SupplierID AND Orders.OrderDate BETWEEN '1996-04-07' AND '1996-12-05' AND Orders.CustomerID = 8

### 7:
SELECT * FROM Customers,Orders,OrderDetails where Customers.CustomerID= Orders.CustomerID and Orders.OrderID=OrderDetails.OrderID and Quantity>50 order by Quantity desc

### 8:
SELECT Products.ProductID, Products.ProductName, Products.SupplierID, Suppliers.SupplierName, Suppliers.ContactName FROM Products INNER JOIN Suppliers ON Products.SupplierID = Suppliers.SupplierID WHERE Suppliers.SupplierName < 'H%' AND Suppliers.ContactName = 'Cheryl Saylor' OR Suppliers.ContactName = 'Chantal Goulet';

### 9:
SELECT FirstName AS Vorname, COUNT(Orders.OrderID) AS AnzahlBestellungen FROM Employees LEFT JOIN Orders ON Employees.EmployeeID = Orders.EmployeeID GROUP BY FirstName

### 10:
SELECT Distinct o.OrderID, Sum(p.price * oD.quantity)  from Orders o, OrderDetails oD, Products p where oD.OrderID = o.OrderID AND p.ProductID = oD.ProductID Group by o.OrderID Having Sum(p.price * oD.quantity) > 2000

### 12:
SELECT Products.ProductID, Products.ProductName, Suppliers.SupplierID, Suppliers.SupplierName, Suppliers.ContactName FROM Products INNER JOIN Suppliers ON Products.SupplierID=Suppliers.SupplierID WHERE (Suppliers.SupplierName > 'A%' AND Suppliers.SupplierName < 'F%') AND (Suppliers.ContactName = "Charlotte Cooper" OR Suppliers.ContactName = "Cheryl Saylor") ORDER BY ProductName ASC;

### 13:
SELECT ord.OrderID,ord.OrderDate,pro.ProductName,pro.Price,odt.Quantity FROM Orders ord JOIN OrderDetails odt ON ord.OrderID = odt.OrderID JOIN Products pro ON odt.ProductID = pro.ProductID WHERE odt.Quantity > 30 ORDER BY pro.ProductName;

### 14:
Select * from (SELECT * FROM Orders o left join OrderDetails od ON o.OrderID = od.OrderID ORDER BY o.OrderID, Quantity DESC) o GROUP BY o.OrderID

### 15:
SELECT OrderID, CustomerID, EmployeeID, MAX(OrderDate), ShipperID FROM Orders
