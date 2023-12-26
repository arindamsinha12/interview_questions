# SQL Coding Interview Questions

I have put together a set of Python coding questions that are typically asked in interviews, drawing on my experience as both interviewer and interviewee. Some of these are questions I have been asked in actual interviews, some are questions from all over the web and I have provided my answers to them irrespective of whether it is the same as the source or not, and some I have simply thought up possible questions in an interview.

I have also create a set of [Coding interview Tips](https://github.com/arindamsinha12/interview_questions/blob/main/coding_interview_tips.md) for coding interviews, which will help avoid typical behavioral mistakes that candidates often make.

My strong suggestion is that anyone using this should try to solve the questions first before looking at the answers in an imaginary interview setting. Give yourself 10 minutes to solve each question.

#### Q1)

A teacher wants to shuffle their students in such a way, that each student in an odd numbered position moves back one seat and each in an even numbered position moves forward one seat. If the last student is in an odd numbered position, leave that unchanged. Based on the table **students** below, write and SQL to do the same.

**Table** ***students***:  
|Position|Name|  
+-------------+  
|1|Alice|  
|2|Ramesh|  
|3|Chan|  
|4|John|  
|5|Rita|  

**Result required:**  
|Position|Name|  
+-------------+  
|1|Ramesh|  
|2|Alice|  
|3|John|  
|4|Chan|  
|5|Rita|  

```
SELECT CASE WHEN position = (SELECT MAX(position) FROM students) AND position % 2 = 1 THEN position
            WHEN position % 2 = 1 THEN position + 1
            ELSE position - 1
       END AS position,
       name
FROM students
ORDER BY position;
```

#### Q2)

From the tables below, list the customers who didn't buy a product and products that did not sell at all.  
The output should be a single list with following columns:  
- The string *customer* or *product* as the case may be  
- The customer id or product id  
- The customer name of product name

**Tables:**  
*Customer*  
|customer_id|customer_name|  
|101|Robert|  
|102|James|  
|103|Amy|  
|104|Shyam|  
|105|Moon|

*Products*  
|product_id|product_name|category|price|  
|1|Box|Packaging|$3.20|  
|2|Belt|Utility|$11.00|  
|3|Table|Furniture|$32.00|  
|4|Chair|Furniture|$16.00|  
|5|Lamp|Utility|$19.00|

*Product_Sales*  
|sale_id|product_id|customer_id|quantity|  
|1|3|101|4|  
|2|4|101|16|  
|3|3|103|1|  
|4|4|103|4|  
|5|5|103|2|  
|6|5|104|1|

```
SELECT 'customer', customer_id, customer_name
FROM customer c
LEFT JOIN product_sales p
USING (customer_id)
WHERE p.customer_id is NULL
UNION
SELECT 'product', product_id, product_name
FROM products pr
LEFT JOIN product_sales p
USING (product_id)
WHERE p.product_id is NULL;
```

#### Q3)

The sales manager wants to know the categories and average prices for categories in which products were sold. Find the same from the above three tables *Customer*, *Products*, and *Product_Sales*.

```
SELECT category, avg(price)
FROM products
WHERE category in (SELECT pr.category
                   FROM products pr
                   JOIN product_sales p
                   using (product_id))
GROUP BY category;
```

*Note: This is one of those slightly tricky questions as I mention in [Coding interview Tips](https://github.com/arindamsinha12/interview_questions/blob/main/coding_interview_tips.md). You do not need the ***Customer*** table at all, nor do you need to output any columns from ***Product_Sales***. This tests the ability to quickly eliminate extraneous information.*
