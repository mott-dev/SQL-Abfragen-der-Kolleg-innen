# SQL-Abfragen-der-Kolleg-innen

## 10
SELECT Distinct o.OrderID, Sum(p.price * oD.quantity)  from Orders o, OrderDetails oD, Products p 
where oD.OrderID = o.OrderID AND p.ProductID = oD.ProductID 
Group by o.OrderID 
Having Sum(p.price * oD.quantity) > 2000
