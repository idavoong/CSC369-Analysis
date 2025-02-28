# Main Question to Answer:
What is the best time to use a rideshare service?
Ex: If I wanted to go from A to B, is it cheaper to book it at 2pm vs 5pm?

To answer this question, I'm planning on using the "required columns". I've also included some "optional columns" that I might use to answer the question because I think it could yield some interesting insights, but isn't necessary to perform the basic analysis. 

# Required Columns for Basic Analysis
- pickup_datetime
- dropoff_datetime
- request_datetime
- on_scene_datetime
- trip_miles
- trip_time
- base_passenger_fare
- congestion_surcharge

# Optional Columns for Further Analysis
- hvfhs_license_num
- tolls
- sales_tax
- tips
- shared_match_flag

# Quality Issues
Some of the columns I'm planning on using for my analysis have NULL values.
### on_scene_datetime
On_scene_datetime describes the time when the driver arrived at the pick-up location. However, this data only exists for accessible vehicles. About ~28% of the data is a NULL value, so I'm deciding to use request_datetime instead. 
### request_datetime
Request_datetime describes the time when the passenger requested to be picked up. About 0.01% of the data is a NULL value. I would just exclude these rows from my analysis since they only make up a small proportion of the entire dataset. 
### congestion_surcharge
Congestion_surcharge is a fee charged to vehicles entering certain areas of NYC during peak hours. About 0.06% of the data is a NULL value. I would also exclude these rows from my analysis because it shouldn't significantly affect the result of my calculations. 