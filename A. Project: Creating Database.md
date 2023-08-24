# PROJECT_1

## Creation of Tables and connections/maintenance

### Table_1.1: products

| product_name | description | costperunit |
|----------|----------|----------|
| TEXT   | VARCHAR(255)   | DECIMAL(10,2)   |

To my knowledge a product table should hold neccesary information about each product. Therefore the basis should be the **product_name** and **costperunit**, as this is fundamentally the foundation of production cost.
Furthermore, if we are to create the table with prudence, we may forsee that dependng on when the product was created the cost might vary. Throughout the years of production, different prices could be set for production and different 3rd parties could be used, as such product will never be constant nor constant cost. However, date cannot be our primary key as two products can be made on the same day. Thus by creating an additional column called **product_id** we can create a primary key unique to ensure no issues caused by overlaps in date or product.

>CREATE TABLE products(  
>product_id SERIAL,  
>production_date DATE NOT NULL,  
>product_name TEXT NOT NULL,  
>description VARCHAR(255),  
>costperunit DECIMAL(10,2) NOT NULL,  
>stock INT NOT NULL,  
>markup DECIMAL(3,2),  
>selling_price DECIMAL(10,2),  
>PRIMARY KEY (product_id)  
>);

**In summary, this is the layout:**  

| | product_id | production_date | product_name | description | costperunit | stock | markup | selling_price   |
|----------|----------|----------|----------|----------|----------|----------|----------|----------|
| *DATA TYPE*   | SERIAL   | DATE   | TEXT   | VARCHAR(255)   | DECIMAL(10,2)   | INT    | DECIMAL(3,2)   | DECIMAL(10,2)   |
| *CONSTRAINT* | PRIMARY KEY | NOT NULL   | NOT NULL  |   | NOT NULL  | NOT NULL  |   |   |


### Table_1.1 Values
Lets test that it works smoothly by adding a test values.

>INSERT INTO products(production_date, product_name, description, costperunit, stock, markup, selling_price)  
>VALUES('2023-08-24','Lenovo Laptop', 'Lenovo Personal Laptop for day-to-day use', 1000, 1, 0.1 , 1100);  
>SELECT * FROM products;

**The result:**
| product_id | production_date | product_name | description | costperunit | stock | markup | selling_price   |
|----------|----------|----------|----------|----------|----------|----------|----------|
| 1   | 2023-08-24   | Lenovo Laptop   | Lenovo Personal Laptop for day-to-day use   | 1000   | 1    | 0.1   | 1100   |

Note that* **description**, **markup** and **selling_price** are not necessary and can be left empty. The reasoning behind this was that some products may be tracked without having a **selling_price**. This way "IN DEVELOPMENT" products can also be included into the products table. I guess my fantasy of complexity relates the costperunit to be a varying value for in developemnt products; likewise, the markup value could be a variable. 

Alternatively, it may be better to opt in a developing_products table to reduce complextiy. Code can then be developed, so that, as soon as the developing_products.completion.value = 1 the row entry is then automatically added to the products table. This would create a seamless system for the sales_team to have access to what they are able sell and the manager can then create a queries connecting the sales table against the products table to see frequently stock levels.  

[DEVELOPMENT OF UPDATING TABLES](https://github.com/cshglobal99/SQL_Collection/blob/main/5.SQL_Advanced.md#automatic-entries)

### Table_1.2: developing_products

Using the above code for updating tables we are able to link the cost of assisiated to development each product per item, to the table of developing projects in the development costs columns.

| | product_id | product_name | latest_update | description | production_cost | stock | complete |
|----------|----------|----------|----------|----------|----------|----------|----------|
| *DATA TYPE*   | SERIAL   |  TEXT  | DATE   | VARCHAR(255)   | DECIMAL(10,2)   | INT    | BOOLEAN    |
| *CONSTRAINT* | PRIMARY KEY | NOT NULL   | NOT NULL  |   | NOT NULL  | NOT NULL  | NOT NULL  |

>CREATE TABLE developing_products(  
>product_id SERIAL,  
>product_name TEXT NOT NULL,  
>latest_update DATE NOT NULL,  
>description TEXT,  
>production_cost DECIMAL(10,2) NOT NULL,  
>stock INT
>complete BOOLEAN NOT NULL, *- To link to the products table*  
>PRIMARY KEY(product_id));

The goal of this table is for **latest_update** and **costperunit** to update using the MAX()/SUM() function on the **development_costs** table, as well as, for when a **complete** entry is "TRUE" for that row to then be transfered into the products table (i.e. copied into products and delted from developing_products). An easy to understand version can be found using the link further above.


### Table_1.3: development_costs

| | product_id | item_order_date | item | item_cost |
|----------|----------|----------|----------|----------|
| *DATA TYPE*   | INT   | DATE   | TEXT   |  INT  |
| *CONSTRAINT* | *FOREIGN KEY & CHECK?* | NOT NULL   | NOT NULL  |
 
>CREATE TABLE development_costs(  
>product_id INT,  
>item_order_date DATE NOT NULL,    
>item TEXT NOT NULL,  
>item_cost DECIMAL(10,2) NOT NULL,  
>FOREIGN KEY(product_id) REFERENCES developing_products(product_id));

Although this will do the job of creating a key and table, using the developed code, we would still be able to enter costs even if developing_products have been transfered over to products. This we need to add a CHECK that will ensure we cannot add a unuvailable product_id (i.e. Developung product 5 has officially been released as product 5. If a new "cost" is found, this should not be included in the development_costs but instead directly to the product's table. We can create this data validation through a CHECK condition).

>>CREATE TABLE development_costs(  
>product_id INT,  
>item_order_date DATE NOT NULL,    
>item TEXT NOT NULL,  
>item_cost DECIMAL(10,2) NOT NULL,  
>FOREIGN KEY(product_id) REFERENCES developing_products(product_id),  
>CHECK (product_id IN (SELECT product_id FROM developing_products));

By adding this "CHECK" condition, we limit the avaiable values so that we can update the developing_products without missing data.

### Table_1.2 Updating developing_products
The updating code was developed [here](), grabbing the sum of **production_costs** from development_costs and inputting, where applicable, in the developing_products.

>UPDATE developing_products AS DevP  
>SET production_cost = (  
>SELECT COALESCE( SUM(item_cost),0)  
>FROM development_costs AS DevC  
>WHERE DevC.product_id = DevP.product_id);  

Similarly we can also do this for the date, but instead of summing we want the max(item_order_date) as this will be our latest product development update.

> PLACEHOLDER FOR CODE


Finally we can also just ensure not costs were not covered by entering the query:

>SELECT DevC.product_id  
FROM development_costs AS DevC  
LEFT JOIN developing_products AS DevP ON DevC.product_id = DevP.product_id  
WHERE DevP.product_id IS NULL;  

### Table 1.3 Updating products

> Code wtill not use Update but instead will only join










### Table_2: sales

>CREATE TABLE sales(  
>sale_id SERIAL PRIMARY KEY,  
>salesperson VARCHAR(100),



### Table_3: client_list





### Table_4: sales_team
