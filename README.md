# EY-repository
This is the code repository for EY


create procedure GetOrderProductCounts
       @OrderCount int
AS
BEGIN
        SELECT
		  p.ProductID,
		  p.ProductName,
		  COUNT(o.OrderID) AS TotalOrders
		FROM
		    Products p
		inner join [Order Details] o on p.ProductID=o.ProductID
		group by 
		  p.ProductID,p.ProductName
		  having
		   count(o.OrderID)>@OrderCount
		order by
		  TotalOrders DESC;
END
 
exec GetOrderProductCounts @OrderCount=2;
