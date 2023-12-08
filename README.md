# Data_Engineering_Coding
My first try in data engineering

The Business Case
Our fictitious company is called Gans. Gans operates an E-Scooter rental service and aims to improve its performance by deploying scooters where they are needed. The task at hand is to determine which areas are more attractive to customers at specific times. To achieve this, we want to obtain predictions for weather and flights from external sources and automate their integration into the company.

Data Collection
The first step is to conduct web scraping via Wikipedia to channel the necessary data about the desired cities. We are interested in the country and coordinates. We need the coordinates to obtain more information about flights and their corresponding airports. For web scraping, an HTML document was downloaded, and the desired data was extracted. The data is stored in a Pandas DataFrame. The result is the DataFrame ‘Cities’, where each row represents a city.

In the next step, data is collected through APIs. A URL is used to send a request for the desired data, using the GET command. JSON is used to represent the data in a usable format. In this case, data from the OpenWeatherMap website is used to provide an overview of the weather in the coming days. The Cities DataFrame, which we created earlier, is used to scan for the corresponding cities. Since OpenWeatherMap provides more information about the weather than we need, the next step involves filtering and creating a reduced DataFrame. 

Next, we want to know when flights arrive at our destinations. To achieve this, we create an account on RapidAPI and use the Endpoints Section of the Aerodatabox API. Using the coordinates of the cities, we scan for surrounding airports. This results in a new static DataFrame that provides us with airports and their airport codes. The airport codes are then used to make a request for arrivals and arrival times at the respective airports. This process creates two more DataFrames. In total, we now have four DataFrames. Cities and Airport Codes are static, and we want the information for Weather and Flights to be updated every day. Therefore, the query for the API endpoints should be automated.

Data Storage
In the next step, the tables are to be pushed into the MySQL Workbench. Connections between the tables should also be established. In SQL, we create tables and name the individual columns just like in the Python script. If everything matches, the data is pushed to SQL with the ‘df.to_sql’ command. Now, if you select SELECT in the SQL Workbench, the table fills with data.

The Cloud
In the next step, the data pipeline is to be transported to the cloud. For this, we need an AWS account. After creating an account, we set up an RDS instance and create a database. It is crucial at all times to keep an eye on AWS costs to ensure that no high bills are incurred. Also, in the MySQL Workbench, a connection must be set up that identifies with the AWS instance. Next, a role is created that allows us to connect with the AWS instance. This enables us to create a Lambda function that executes the entire process. The Lambda function incorporates the functions created earlier on our local level. It ensures that the Weather and Flights tables are automatically updated. Additionally, we can set up a trigger in AWS to update the tables in MySQL at a specific time.

The company can now see when many people are coming to the cities and need a scooter or when the weather is good, and the demand for scooters is higher than in bad weather. Therefore, the company can deploy the scooters to the right place at the right time with delivery vehicles, not only increasing rides and revenue but also enhancing customer satisfaction as customers no longer have to search for scooters for a long time. 
