# Customer-Segmentation-

--What is the distribution of order values across all customers in the dataset?
	
SELECT CustomerID,
UnitPrice/Quantity AS total_order_value
FROM [dbo].['Online Retail$']
WHERE CustomerID IS NOT NULL
ORDER BY total_order_value DESC;

--How many unique products has each customer purchased?

SELECT CustomerID, StockCode AS Unique_StockCode, Description
FROM [dbo].['Online Retail$']

--Which customers have only made a single purchase from the company?

SELECT CustomerID, count(StockCode) AS Unique_StockCode
FROM [dbo].['Online Retail$']
GROUP BY CustomerID
HAVING count(Quantity) = 1;


--Which products are most commonly purchased together by customers in the dataset?


SELECT online1.StockCode, online2.StockCode, COUNT(*) AS Purchase_frequency
FROM [dbo].['Online Retail$'] AS online1
INNER JOIN [dbo].['Online Retail$'] AS online2
ON online1.CustomerID = online2.CustomerID
AND online1.InvoiceNo = online2.InvoiceNo
AND online1.StockCode < online2.StockCode
GROUP BY online1.StockCode, online2.StockCode
