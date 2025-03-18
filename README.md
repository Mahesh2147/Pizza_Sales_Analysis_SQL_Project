# Pizza_Sales_Analysis_SQL_Project

### 🍕 Summary of Pizza Sale SQL File

# 1️⃣ Database Creation: pizzahut
	CREATE DATABASE pizzahut;
* Insight: Creates a database named pizzahut to store all related data.

# 2️⃣ Orders Table Definition
	CREATE TABLE orders (
	                    order_id INT NOT NULL,
	                    order_date DATE NOT NULL,
	                    order_time TIME NOT NULL,
 		                  PRIMARY KEY(order_id)
	  );
* Insight:

   * Stores order details with the following columns:
  
      * order_id: Unique identifier for each order.

      * order_date: Date of the order.

      * order_time: Time when the order was placed.

# 3️⃣ Order Details Table Definition
    CREATE TABLE order_details (
                        		    order_details_id INT NOT NULL,
                        		    order_id INT NOT NULL,
                        		    pizza_id TEXT NOT NULL,
                        		    quantity INT NOT NULL,
                        		    PRIMARY KEY(order_details_id)
		  );
* Insight: Stores item-level details for each order.
  
  * Contains:

      * order_details_id: Unique identifier for each order detail.

      * order_id: Links to the orders table.

      * pizza_id: Identifies the pizza ordered.

      * quantity: Number of pizzas ordered.

📊 Basic Queries:

# 1️⃣ Total Number of Orders Placed
  	SELECT COUNT(order_id) AS total_orders
		FROM orders;
* Insight:

    * Counts the total number of orders placed.

  	* Useful for tracking overall order volume.

# 2️⃣ Total Revenue Generated from Pizza Sales
	SELECT 
	    ROUND(SUM(order_details.quantity * pizzas.price), 2) AS total_sales
	FROM 
	    order_details
	JOIN 
	    pizzas ON pizzas.pizza_id = order_details.pizza_id;
* Insight:

  * Calculates total sales revenue by multiplying quantity by price.

  * Helps assess overall revenue performance.

# 3️⃣ Highest-Priced Pizza
		SELECT 
		    pizza_types.name, pizzas.price
		FROM 
		    pizza_types
		JOIN 
		    pizzas ON pizza_types.pizza_type_id = pizzas.pizza_type_id
		ORDER BY pizzas.price DESC
		LIMIT 1;
	
 * Insight:

    * Identifies the most expensive pizza on the menu.

    * Useful for premium product positioning.

# 4️⃣ Most Common Pizza Size Ordered
  	SELECT 
		    pizzas.size,
		    COUNT(order_details.order_details_id) AS order_count
		FROM 
		    pizzas
		JOIN 
		    order_details ON pizzas.pizza_id = order_details.pizza_id
		GROUP BY 
		    pizzas.size
		ORDER BY 
		    order_count DESC;
	
 * Insight:

    * Identifies the most popular pizza size.

    * Useful for inventory and sales optimization.

# 5️⃣ Top 5 Most Ordered Pizza Types with Quantities
		SELECT 
		    pizza_types.name, SUM(order_details.quantity) AS quantity
		FROM 
		    pizza_types
		JOIN 
		    pizzas ON pizza_types.pizza_type_id = pizzas.pizza_type_id
		JOIN 
		    order_details ON pizzas.pizza_id = order_details.pizza_id
		GROUP BY 
		    pizza_types.name
		ORDER BY 
		    quantity DESC
		LIMIT 5;
* Insight:

    * Lists the top 5 best-selling pizza types.

    * Useful for identifying customer preferences.

# 🎯 Overall Summary:
	
* Sales Insights: Track revenue, order trends, and product performance.

* Menu Analysis: Identify popular items and premium offerings.

* Customer Preferences: Analyze size and type preferences to optimize inventory and promotions.
