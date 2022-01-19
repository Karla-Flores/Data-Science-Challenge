<h1>Data Science Challenge</h1>

<h3>Question 1</h3>
<hr>

Given some sample data, write a program to answer the following:

On Shopify, we have exactly 100 sneaker shops, and each of these shops sells only one model of shoe. We want to do some analysis of the average order value (AOV). When we look at orders data over a 30 day window, we naively calculate an AOV of $3145.13. Given that we know these shops are selling sneakers, a relatively affordable item, something seems wrong with our analysis. 

<ul>
<li><b>Think about what could be going wrong with our calculation. Think about a better way to evaluate this data.</b></li>
The initial calculation considers the mean of all order amount. However, while exploring the data, outliers have impacted the final result, like the user_id 607 with an average purchase amount of $70 4000.0. Or the order_id 692 and 3725 with $154 350 and $77 175 respectively. Another outlier was the shop_id 78, with a purchase average of $46 188.06.
<p></p> 
After removing those, the new AOV should be $151.68.
<p></p>  
<li><b>What metric would you report for this dataset?</b></li>
I would use the median of the middle 50% of the dataset. This new metric would allow me to consider only the values that make up the middle 50% of the dataset (thereby dropping from consideration values that are very low or very high).
<p></p>
<li><b>What is its value?</b></li>
280.0
</ul>
<p></p>
<h3>Question 2</h3>
<hr>

For this question you’ll need to use SQL. Follow <a href='https://www.w3schools.com/SQL/TRYSQL.ASP?FILENAME=TRYSQL_SELECT_ALL'>this link</a> to access the data set required for the challenge. Please use queries to answer the following questions. Paste your queries along with your final numerical answers below.

<ul>
<li><b>How many orders were shipped by Speedy Express in total?</b></li>
Code: <br>
SELECT COUNT(Orders.OrderID) as 'Speedy Count'
FROM Orders INNER 
JOIN Shippers 
ON Orders.ShipperID=Shippers.ShipperID 
WHERE Shippers.ShipperName = 'Speedy Express';
<p></p>
In total, 54 orders were shipped by Speedy Express.  
<p></p>  
<li><b>What is the last name of the employee with the most orders?</b></li>
Code: <br>
(SELECT *, COUNT(DISTINCT OrderID) AS NetOrders 
FROM (SELECT o.OrderID, e.EmployeeID, e.LastName, e.FirstName
FROM Orders o Inner JOIN Employees e
ON o.EmployeeID = e.EmployeeID)
GROUP BY EmployeeID
ORDER BY COUNT(DISTINCT OrderID) DESC);
<p></p>  
The last name of the employee is Peacock, and the number of orders is 40.
<p></p>
<li><b>What product was ordered the most by customers in Germany?</b></li>
Code:<br>
SELECT p.ProductName, SUM(Quantity) AS TotalQuantity
FROM Orders AS o, OrderDetails AS od, Customers AS c, Products AS p
WHERE c.Country = "Germany" AND od.OrderID = o.OrderID AND od.ProductID = p.ProductID AND c.CustomerID = o.CustomerID
GROUP BY p.ProductID
ORDER BY TotalQuantity DESC
LIMIT 1;
<p></p>
Boston Crab Meat is the product with a total of 160 orders.
</ul>
