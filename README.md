# Airline_Delay

## Selected Topic

***Airline Delay***

Google Slide Presentation can be viewed [here.](https://docs.google.com/presentation/d/1Gdb_rvwP0_uNhjOWyThWgazxaziDxe8qXib3i6_Qr8g/edit#slide=id.g13c2af1fd4b_2_26144)

## Reason
COVID-19 once stalled much of airline businesses as travel became scarce. In recent months, especially since it has become warm and people are going on summer holidays, airline travel has resumed. However, we've noticed that there are more and more delays in flights that often mess up people's schedules. We are curious to know in more detail which airlines have more delays, which airports, and which flights (origin - destination) are causing more of the delay data.

## Description of the source of data
Airlines dataset has 539383 instances and 8 different features. 

Columns include: 
- I. Airline 
- II. Flight 
- III. Airport From 
- IV. Airport To 
- V. DayOfWeek 
- VI. Time
- VII. ID
- VIII. Length 
- IX. Delay

## Initial Questions we hoped to answer with the data
The initial goal of this project is to build a flight delay prediction model that predicts whether a flight will be delayed depending on factors such as: 

- Airline
- Departing Airport
- Day of Week 
- How long a flight will be delayed

However, we quickly realized that the above would be difficult to predict based on the given information in the dataset. Additionally, some of the columns were unclear: specifically the "Time" column. So this column was dropped. 

## Data Exploration Phase

- Downloaded into Jupyter Notebook
- N/A (null) rows removed
- Identified count of 18 different Airlines
- Identified count of 293 Airports (all domestic flights)
- Changed DayOfWeek numerical values to corresponding day 
- Dropped “Time” column
- Create new DataFrame and export to CSV and DB


## Data Analysis Phase

- Compare delayed frequency between departing airports 
- Compare delayed frequency by Airline 
- Create regression model to predict flight delay based on airline, departing airport, arriving airport, and day of week with decision trees. 
- Sort features by their importance 

## Machine Learning Model 

***Supervised Learning - Logistic Regression Classification Model***
After exploring the data we decided to proceed with a Logistic Regression Classification Model  mainly because we narrowed down our goal from including continuous variables to only attempting to predict a binary outcome - "delayed" and "not delayed". 

### SEGMENT 2

***Description of preliminary data preprocessing***
Data preprocessing included data cleanup such as converting the numbered days of week to the actual day of the week within the DataFrame. 

***Description of preliminary feature engineering and preliminary feature selection, including their decision-making process***

At first, we selected features as all columns except the target column which is the "delay" column. However, we weren't 100% certain what the "Time" column indicated. Therefore, we removed the time column, flight number, and ID column and created a new DataFrame. Within that new DataFrame, our target column remained the same and our features became Length, Airline, AirportFrom, AirportTo, DayOfWeek.

***Description of how data was split into training and testing splits***
We split the data into training and testing sets - used random_state to make the data reproducible and ensure that same rows are assigned to train and test sets. "X" was assigned to our features and "y" was assigned to our target "delay".


***Explanation of model choice, including limitations and benefits***
Random Forest Classified was chosen because of its ability to rank importance of input variables, run efficiently on larger datasets, and its robustness against overfitting. However, some limitations include slowness which makes the model ineffective for real-time predictions. 

***Explanation of how model was trained***
Data was split into training and testing sets. Random state = 1 was used to make the data reproducible and ensure that the same rows are assigned to corresponding train and test sets. Data was trained using random forest classifier.

## Database

The Link to the Database downloaded can be found [here.](https://www.kaggle.com/datasets/jimschacko/airlines-dataset-to-predict-a-delay?datasetId=2285093&group=owned)

### SEGMENT 2

Column titles were update as well as 2 tables created. Table 1 is the features table with a converted DayOfWeek column that lists a string of the actual weekday. Table 2 is our target table that includes the airline abbreviations and delay. 

We originally decided to keep all columns as features (except delay). We felt that these columns would best fit the questions we are aiming to answer with the unique identified being flight number. These include: 
- Flight
- airline
- departing_airport
- arrival_airport
- weekday
- delay_mins
- flight_length

 We created a connection between sqlite3 and Airlines.db, then addded features_df and target_df to this database. After this, we commited the connection and then executed sql databse in SQLiteStudio. The tables were merged as an OUTERJOIN to complete the full table as this adds the delay column and includes the airlines. 

![airlines_db_join.png](airlines_db_join.png)

## Dashboard

###### TOOLS THAT WILL BE USEFUL TO CREATE THE FINAL DASHBOARD
- Tableau
- Machine Learning model

###### DESCRIPTION OF INTERACTIVE ELEMENT

There will be two to three main components to the ***Dashboard***, 
- An interactive map of the U.S. where data points/analysis will show when user hovers over certain locations (and when user clicks into the state, they will be shown to a new page(?) of more details and probability of flight delay

- Percentages and table rankings of different metrics that is live and connected to the ML model (i.e. "top airports with most delays", "worst airlines to fly on based on delays within last x days", etc.)

