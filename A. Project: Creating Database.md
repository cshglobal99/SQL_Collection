# PROJECT_1

## Creation

### Table_1: products

To my knowledge a product table should roughly hold basic neccesary information per product. Therefore the base should be the **product_name** and **costperunit**, as this is fundamentally the foundation of production cost.
Furthermore, if we are to create the table with prudence, we may forsee that the cost might depend on the date of production.
Thus by creating an additional column called **product_id** we can create a primary key unique to ensure no issues caused by overlaps in date or product.

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


### Table_1 Values
Lets test that it works smoothly by adding a test values.

>INSERT INTO products(production_date, product_name, description, costperunit, stock, markup, selling_price)  
>VALUES('2023-08-24','Lenovo Laptop', 'Lenovo Personal Laptop for day-to-day use', 1000, 1, 0.1 , 1100);  
>SELECT * FROM products;

**The result:**
| product_id | production_date | product_name | description | costperunit | stock | markup | selling_price   |
|----------|----------|----------|----------|----------|----------|----------|----------|
| 1   | 2023-08-24   | Lenovo Laptop   | Lenovo Personal Laptop for day-to-day use   | 1000   | 1    | 0.1   | 1100   |

*Note that* **description**, **markup** *and* **selling_price** *are not necessary and can be left empty. The reasoning behind this was that some products may be tracked without having a* **selling_price**. *This way "IN DEVELOPMENT" products can also be included into the products table.

I guess my fantasy of complexity relates the costperunit to be a varying value for in developemnt products; likewise the markup value could be a variable. Alternatively it may be better to opt in a developing_products table to reduce complextiy, and as soon as the developing_products.completion.value = 1 the row entry is then automatically added to the products table for the sales_team to have access to what they can sell.*  
**This Marks the end of Table_1 creation**

### Table_2: sales

>CREATE TABLE sales(  
>sale_id SERIAL PRIMARY KEY,  
>salesperson VARCHAR(100),



### Table_3: client_list





### Table_4: sales_team
