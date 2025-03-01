# Main Question to Answer:
What is the best time to use a rideshare service?
Ex: If I wanted to go from A to B, is it cheaper to book it at 2pm vs 5pm?

To answer this question, I anticipate I will need to use the "required columns". I've also included some "optional columns" that I might use to answer the question because I think it could yield some interesting insights, but isn't necessary to perform the basic analysis. 

### Required Columns for Basic Analysis
- pickup_datetime
- dropoff_datetime
- request_datetime (won't be using anymore - see quality issues #4)
- on_scene_datetime (won't be using anymore - see quality issues #4)
- trip_miles
- trip_time
- base_passenger_fare
- congestion_surcharge

### Optional Columns for Further Analysis
- hvfhs_license_num 
- tolls
- sales_tax
- tips
- shared_match_flag

# Data Parsing
The dataset is already structured in multiple parquet files, so I don't believe I need to parse it into another format. I will be using "{file_path}/*.parquet" so that my SQL queries will run on all of the parquet files.   


# Quality Issues

Some of the columns I'm planning on using for my analysis have NULL values.
### 1. on_scene_datetime
On_scene_datetime describes the time when the driver arrived at the pick-up location. However, this data only exists for accessible vehicles. About ~28% of the data is a NULL value, so I'm deciding to use pickup_datetime instead. 
### 2. request_datetime
Request_datetime describes the time when the passenger requested to be picked up. About 0.01% of the data is a NULL value. I would just exclude these rows from my analysis since they only make up a small proportion of the entire dataset. 
### 3. congestion_surcharge
Congestion_surcharge is a fee charged to vehicles entering certain areas of NYC during peak hours. About 0.06% of the data is a NULL value. I would also exclude these rows from my analysis because it shouldn't significantly affect the result of my calculations. 

Other concerns:
### 4. pickup_datetime vs request_datetime vs on_scene_datetime
Pickup_datetime: The date and time of the trip pick-up   
Request_datetime: date/time when passenger requested to be picked up   
On_scene_datetime: date/time when driver arrived at the pick-up location (Accessible Vehicles-only)   
I'm deciding to use pickup_datetime to calculate the length of trips over the other variables. Request_datetime seems a little ambigious since the time a user requested to be picked up doesn't necessarily mean that they were picked up during that time. As for on_scene_datetime, a good amount of data for the column is missing. I'm also unsure if the time the driver was in the area is related to the length of the trip, because there are some areas (like airports) where drivers are usually waiting for a customer.   
I checked if there were any instances where pickup_datetime is after dropoff_datetime, and it was less than 0.01% of the entire dataset. I will be excluding these instances from my analysis by filtering. 