# Databricks SQL Lab

- Bitly - https://bitly.com/
- LeapChat - https://www.leapchat.org/

## Setup
### CLICK >> [Lab Env Registration Link](https://labs.databricks.com/#/odl/b1c44777-dce6-4a70-a7c4-cd5766ea2a02)

### Hail Mary Assets
- [Lab Env Registration Link](https://labs.databricks.com/#/odl/b1c44777-dce6-4a70-a7c4-cd5766ea2a02)
- [Lab Workspace URL](https://dbc-7799459f-0ccf.cloud.databricks.com/)
- [Link to PDF of slides]()
- [LeapChat Room]()
- [Repo Link](https://github.com/Zaxier/dbsql_lab_instructions)
- *My LeapChat screen name*:   `XavierTheArbiterOfTruth`
- *My email address*: `xavier@databricks.com`

## Lab Context: What are we going to do?
- Use Databricks SQL to analyze two datasets
    1. NYC Taxi Trip Analysis - from *NYC Taxi and Limousine Commission*
    2. Retail Revenue and Supply Chain data - from *TPC-H benchmark*
- In doing that we will get comfortable navigating the Databricks SQL UI and the capabilities of the platform.

## Dataset description

### NYC Taxi Trips
The NYC Taxi data set is a popular data set containing trip records from taxi rides in New York City. It includes information such as the pickup and drop-off locations, trip distances, fare amounts, payment types, and more. The data set has been used for a variety of purposes, including transportation planning, predictive modeling, and data visualization. The dataset is a single table.

### TPC-H (Retail Revenue and Supply Chain data)
The TPC-H dataset is significant in the database industry as it provides a standardized benchmark for evaluating the performance of decision support systems and analytical database systems. The benchmark consists of a set of complex SQL queries that simulate real-world business scenarios, and is designed to test the performance of systems that handle large volumes of data and complex queries.

The TPC-H dataset includes a schema and set of tables that represent various aspects of a business, including customers, orders, line items, suppliers, parts, and nations. The data model is a star schema, where the fact table (lineitem) is connected to several dimension tables (customer, orders, supplier, part, and nation) through foreign keys.

The tables and their relationships in the TPC-H dataset are as follows:
- `customer`: Contains information about customers, including their name, address, phone number, and account balance.
- `orders`: Contains information about orders, including the order date, customer ID, order priority, and ship date.
- `lineitem`: Contains information about individual items in each order, including the quantity, price, and discount for each item.
- `supplier`: Contains information about suppliers, including their name, address, and phone number.
- `part`: Contains information about parts, including their name, brand, size, and supplier ID.
- `nation`: Contains information about countries, including the country name, region, and population.

## Instructions

### Exercise 0: Understand the datasets 
1. Either read the above descriptions or use chatGPT (https://chat.openai.com/chat) and ask about the NYC Taxi dataset. Ask chatGPT why it is a an important or useful data set or benchmark and why it is used in industry.
2. Ask chatGPT about the TPC-H dataset. Ask chatGPT why it is a an important or useful data set or benchmark and why it is used in industry.

### Exercise 1: DBSQL Navigation.
1. Navigate to SQL Persona (top-left)
2. Click on "Data" in the LHS panel. Navigate to the `samples` catalog.
3. Explore the two schemas [`nyctaxi`, `tpch`] in the Data Explorer
    - Review the schemas of the tables within each.
4. Create a quick dashboard 
    - To do this, navigate to the `nyctaxi.trips` table within the Data Explorer, click "Create" and choose "Quick Dashboard". Go forth from there to shape the dashboard.
5. Create a query and use the SQL Editor
    - Navigate to the `nyctaxi.trips` table within the Data Explorer, click "Create" and choose "Query".
    - Run the `SELECT *` query and inspect the results.
6. Create a schema to store tables and views
    - Create the schema in the hive_metastore catalog [docs link](https://docs.databricks.com/sql/language-manual/sql-ref-syntax-ddl-create-schema.html)
    - Run a CTAS (`CREATE TABLE AS SELECT`) query to create a new table in your new schema. [example](https://docs.databricks.com/sql/language-manual/sql-ref-syntax-ddl-create-table-using.html#:~:text=%2D%2D%20Use%20data%20from%20another%20table%0A%3E%20CREATE%20TABLE%20student_copy%20AS%20SELECT%20*%20FROM%20student%3B)
    - Create a view in your new schema. [example](https://docs.databricks.com/sql/language-manual/sql-ref-syntax-ddl-create-view.html)
7. Write a more complex query with the help of code completion. Answer the following questions using SQL and the `nyctaxi.trips` table:
    - Find the average fare_amount percentage for each day of the week:
    - Find the number of trips and average trip distance for each hour of the day

You can use chatGPT if you like! It know about the NYC taxi dataset. If you tell it your table name and column names it might help too.

For example
```sql
SELECT
  DAYOFWEEK(tpep_pickup_datetime) AS day_of_week,
  COUNT(*) AS num_trips,
  SUM(fare_amount) AS fare_amount
FROM
  trips
GROUP BY
  day_of_week;
```
8. Name, save and share a query
    - Name the query (in the SQL Editor UI)
    - Save the query (in the SQL Editor UI)
    - Share the query (in the SQL Editor UI) with another user or all users.
    - Locate the saved query in your "Workspace" browser and the "Queries" browser (both available on the LHS panel).
    - Organise the query into a folder

### Exercise 2: Dashboards ([docs](https://docs.databricks.com/sql/user/dashboards/index.html))
1. Navigate to SQL Persona (top-left)
2. On the DBSQL Home Page, under "Sample dashboards", click "Visit gallery".

**Explore the NYC Taxi dashboard**
1. Import the NYC Taxi dashboard on the DBSQL Home page.
4. Dashboard should open automatically (if not navigate to Dashboard from LHS Panel)
6. Use the widgets to filter the data.
    - How many trips (pickups) were there from zip code 11222 in January 2016
7. Choose a visualisation, enlarge it and inspect the data.
8. Choose a visualisation, at the top right of the visualisation, click on the "..." and choose "View query"
9. Inspect the query, run it, 
10. Notice the visualisations tabbed under the editor next to the table results. 
11. Edit the query or the visualisation and notice the results update.

**Explore the Retail Supply Chain Dashboard**
1. Import the Retail Supply Chain dashboard on the DBSQL Home page.
2. Dashboard should open automatically (if not navigate to Dashboard from LHS Panel)
3. Update the **Most Valuable Customers** visualisation so that it orders by the revenue of the customer. 
    - Do this by editting the query backing visualisation. I.e. click on the "..." next to the visualisation and choose "View query".
    - Edit the query by adjusting the `order by` clause in the query, so that the ordering for the results and visualisation uses `total_revenue` descending. ie. `order by total_revenue desc`.
    - Run the query and confirm the results. The customer with the highest revenue should be `721180`.
4. Update the **Global Revenue Analyses** visualisation so that it's easier to read. 
    - Do this by editting the query backing visualisation. I.e. click on the "..." next to the visualisation and choose "View query".
    - The results table and the visualisation will be visible in the bottom panel. Choose the visualisation and edit it. Within the visualisation editor, change the Colors. Choose 'Max color' to be a high contrast red. This makes the visualisation easier to read.
6. Save the visualisation then navigate back to the dashboard and refresh the browser window. The visualisation should now be updated with the higher contrast red for the USA, UK, Saudi Arabia etc who have the highest revenue.

### Exercise 3: SQL Analytics
In this exercise we will write SQL to analyse the TPC-H dataset, and then add visualisations to the existing dashboard.

1. Use chatGPT and ask about the TPC-H dataset. Ask chatGPT why it is a an important or useful data set or benchmark and why it is used in industry.
2. Ask chatGPT to suggest some questions that can be answered using the TPC-H dataset.
3. Ask chatGPT to provide the SQL to answer these questions for you mentioning the TPC-H dataset in your prompt.
4. Copy the SQL into the SQL Editor and run the query. Note, you may have to update syntactical elements of the SQL to make it work in DBSQL. GOOD NEWS: We're creating a dedicated chatbot for querying tables within the lakehouse that will produce the correct SQL for you.
5. Choose 3-4 queries and produce 3-4 visualisations. 
6. Save and name the queries.
6. Create a dashboard and add the visualisations to it.
    - Navigate to the "Dashboards" browser (available on the LHS panel)
    - Create a new dashboard and provide a name.
    - Click "Add" and choose the visualisations you want to add. They will be searchable by the query names first and visualisation name second.
    - When you're done, click "Done editing" and then click "Share" and share the dashboard with all users of the workspace.
7. Volunteers to talk through their visuals!

### Exercise 4: Infrastructure Monitoring
1. Within DBSQL, click on "SQL Warehouses" on the LHS panel.
2. Choose the running serverless warehouse.
3. Click on monitoring and inspect the metrics.

### Exercise 5: Spam the chatroom with
1. Rating out of 10 for the session
2. What did you like?
3. What could be improved?
4. Memes and general spamming encouraged.

### Extras
5. Check out the news about Dolly, Databricks' open-source large language model.
    - https://www.databricks.com/blog/2023/03/24/hello-dolly-democratizing-magic-chatgpt-open-models.html
    - https://www.bing.com/news/search?q=Dolly+Databricks&qpvt=dolly+databricks&FORM=EWRE
6. Check out the Databricks blog:
    - https://www.databricks.com/blog
    - Navigate using the sub-blogs on the LHS (check out your industry, or the one you're interested in).
