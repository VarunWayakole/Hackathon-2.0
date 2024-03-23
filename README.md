# Hackathon-2.0

**Problem Statement:**
GDS Grands owns multiple five-star hotels across India. They have been in the 
hospitality industry for the past 20 years. Due to strategic moves from other 
competitors and ineffective decision-making in management, GDS Grands are 
losing its market share and revenue in the luxury/business hotels category. 
As a strategic move, the managing director of GDS Grands wanted to 
incorporate “Business and Data Intelligence” in order to regain their market share 
and revenue. However, they do not have an in-house data analytics team to 
provide them with these insights.
Their revenue management team had decided to hire a 3rd party service provider 
to provide them insights from their historical data.

**Dataset:**

1. dim_date
2. dim_hotels
3. dim_rooms
4. fact_aggregated_bookings
5. fact_bookings

**Steps**:

**1. Load data into Power BI:**

   Open Power BI - Get Data - Link Folder which contains csv files - convert binary to tables

**2. Data Transformation:**

   Used first row as header
   Generated a new column in dim_date table called "week number" to determine week numbers from dates
         - Dax formula: week_number = WEEKNUM(dim_date[date])

  Changed "day_type" column values -> considering Saturday or Sunday as Weekend
         - Dax formula: day_type = IF(WEEKDAY(dim_date[Date], 2) >= 6, "Weekend", "Weekday")

**3. Managed Relationships:**
  Created star schema relationship between tables
![StarSchema](https://github.com/VarunWayakole/Hackathon-2.0/assets/91410941/f31e1950-b33d-4c4a-b68a-7810ffdd9f9b)
