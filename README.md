# ETL-Pipeline-using-AWS-Redshift

Banks have to refill the ATMs when the money goes below a specific threshold limit. 

This depends on the activity and the area where a particular ATM is located as well as the weather, day of the week, etc.

Spar Nord Bank is trying to observe the withdrawal behaviour and the corresponding dependent factors to optimally manage the refill frequency. Apart from this, other insights also have to be drawn from the data.

 
Your overall task in this project will be to build a batch ETL pipeline to read transactional data from RDS, transform and load it into target dimensions and facts on Redshift Data Mart(Schema).
We have data from more than 100 ATMs across Denmark. Data is captured for every transaction including, card type, location, date, time, ATM type, etc.

Also, the transaction amount field in the data set was added separately using a random function for the analysis purpose. 

Spar Nord Bank has also built a dimensional model datastore (ATM Data Mart) on this ATM transaction data to understand the ATM usage pattern. This exact schema(target schema) of this Data Mart will be provided to you for the sake of this project. Basically, this will be the schema according to which you will be creating tables in Redshift. 

Broadly you will be performing the following task-

Extracting the transactional data from a given MySQL RDS server to HDFS(EC2) instance using Sqoop.

Transforming the transactional data according to the given target schema using PySpark. 

This transformed data is to be loaded to an S3 bucket.

Creating the Redshift tables according to the given schema.

Loading the data from Amazon S3 to Redshift tables.

Performing the analysis queries as below:


Top 10 ATMs where most transactions are in the ’inactive’ state

Number of ATM failures corresponding to the different weather conditions recorded at the time of the transactions

Top 10 ATMs with the most number of transactions throughout the year

Number of overall ATM transactions going inactive per month for each month

Top 10 ATMs with the highest total amount withdrawn throughout the year

Number of failed ATM transactions across various card types

Top 10 records with the number of transactions ordered by the ATM_number, ATM_manufacturer, location, weekend_flag and then total_transaction_count, on weekdays and on weekends throughout the year

Most active day in each ATMs from location "Vejgaard"

*******************************************************************************************************************************************************************
you will be working on a Danish ATM Transactions Data Set in this project.
This dataset comprises around 2.5 million records of withdrawal data along with weather information at the time of the transactions from around 113 ATMs from the year 2017.

The actual data set is divided into two part files, both amounting to about 503 MB in total. 

There is also a data dictionary present along with the data set, which defines all of the 33 columns present in the data set. The data dictionary is given below.
This data set contains various types of transactional data as well as the weather data at the time of the transaction, such as:

Transaction Date and Time: Year, month, day, weekday, hour

Status of the ATM: Active or inactive

Details of the ATM: ATM ID, manufacturer name along with location details such as longitude, latitude, street name, street number and zip code

The weather of the area near the ATM during the transaction: Location of measurement such as longitude, latitude, city name along with the type of weather, temperature, pressure, wind speed, cloud and so on

Transaction details: Card type, currency, transaction/service type, transaction amount and error message (if any)
 
[ETL+Project+-+RDS+Data+dictionary.pdf](https://github.com/pshru22/ETL-Pipeline-using-AWS-Redshift/files/9623800/ETL%2BProject%2B-%2BRDS%2BData%2Bdictionary.pdf)

*******************************************************************************************************************************************************************
Target schema:

For this project, you will need four dimension tables and one fact table. They are as follows:

ATM dimension - This dimension will have the data related to the various ATMs present in the dataset along with the ATM number(ATM ID in the original dataset), ATM manufacturer and a reference to the ATM location and is very important for solving analytical queries related where ATM data will be used.

Location dimension - This is a very important dimension containing all the location data including location name, street name, street number, zip code and even the latitude and longitude. This information will be very important for solving problems related to the particular location at which a transaction took place and can help banks in things like pinpointing locations where ATMs where demand is higher as compared to other locations. Combined with weather data in the transaction table, this can be used to further do analysis such as how weather affects the demand at ATMs at a particular location.

Date dimension - This is another very important dimension which is almost always present where data such as transactional data is being dealt with. This dimension includes fields such as the full date and time timestamp, year, month, day, hour as well as the weekday for a transaction. This all can help in analysing the transaction behaviour with respect to the time at which the transaction took place and also how the transaction activity varies between weekdays and weekends.

Card type dimension - This dimension has the information about the particular card type with which a particular transaction took place. This can help in performing analysis on how the number of transactions varies with respect to each different card type.

Transaction fact - This is the actual fact table for the data set which contains all of the numerical data such as the currency of the transaction, service, transaction amount, message code and text as well as weather info such as description, weather id etc.
![target_schema](https://user-images.githubusercontent.com/73575402/191696022-1c054416-70a2-46da-9844-dc88ed191d3b.JPG)
[ETL+Project_+Schema+for+Dimensions+and+Fact.pdf](https://github.com/pshru22/ETL-Pipeline-using-AWS-Redshift/files/9623825/ETL%2BProject_%2BSchema%2Bfor%2BDimensions%2Band%2BFact.pdf)
[ETL+Project+Hint+Document.pdf](https://github.com/pshru22/ETL-Pipeline-using-AWS-Redshift/files/9623830/ETL%2BProject%2BHint%2BDocument.pdf)
[ETL+Project+-+Validation+Document+V1.pdf](https://github.com/pshru22/ETL-Pipeline-using-AWS-Redshift/files/9623831/ETL%2BProject%2B-%2BValidation%2BDocument%2BV1.pdf)
