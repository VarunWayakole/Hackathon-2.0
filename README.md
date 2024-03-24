# Hackathon-2.0

**Problem Statement:**
<p align="justify">GDS Grands owns multiple five-star hotels across India. They have been in the 
hospitality industry for the past 20 years. Due to strategic moves from other 
competitors and ineffective decision-making in management, GDS Grands are 
losing its market share and revenue in the luxury/business hotels category. 
As a strategic move, the managing director of GDS Grands wanted to 
incorporate “Business and Data Intelligence” in order to regain their market share 
and revenue. However, they do not have an in-house data analytics team to 
provide them with these insights.
Their revenue management team had decided to hire a 3rd party service provider 
to provide them insights from their historical data.</p>

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

   Generate a new column in dim_date table called "week number" to determine week numbers from dates<br>
         - Dax formula: week_number = WEEKNUM(dim_date[date])

   Change "day_type" column values -> considering Saturday or Sunday as Weekend<br>
         - Dax formula: day_type = IF(WEEKDAY(dim_date[Date], 2) >= 6, "Weekend", "Weekday")

**3. Manage Relationships:**

   Create a star schema relationship between tables
   ![StarSchema](https://github.com/VarunWayakole/Hackathon-2.0/assets/91410941/f31e1950-b33d-4c4a-b68a-7810ffdd9f9b)

**4. Create measures:**

   Revenue - SUM(fact_bookings[revenue_realized])<br>
   Total Bookings - COUNT(fact_bookings[booking_id])<br>
   Average Rating - AVERAGE(fact_bookings[ratings_given])<br>
   Total Capacity - SUM(fact_aggregated_bookings[capacity])<br>
   Total Succesful bookings - SUM(fact_aggregated_bookings[successful_bookings])<br>
   Occupancy % - DIVIDE([Total Succesful bookings], [Total Capacity], 0)<br>
   Total Cancelled Bookings - CALCULATE([Total Bookings], fact_bookings[booking_status] = "Cancelled")<br>
   Cancellation Rate - DIVIDE([Total cancelled bookings], [Total Bookings], 0)<br>
   
   Other Key Measures:<br>
   Average Daily Rate - DIVIDE([Revenue], [Total Bookings], 0)<br>
   Booking % by Platform - DIVIDE([Total Bookings], CALCULATE([Total Bookings], ALL(fact_bookings[booking_platform]))) * 100<br>
   No of Days - DATEDIFF(MIN(dim_date[date]), MAX(dim_date[date]), DAY) + 1<br>
   Daily Booked Room (DBR) - DIVIDE([Total Bookings], [No of Days], 0)<br>
   Revenue Per Available Room - DIVIDE([Revenue], [Total Capacity], 0)<br>
   Daily Sellable Rooms - DIVIDE([Total Capacity], [No of Days], 0)<br>
   Daily Utilized Rooms - DIVIDE([Total Checked Out], [No of Days], 0)<br>
   Total No Show Bookings - CALCULATE([Total Bookings], fact_bookings[booking_status] = "No Show")<br>
   No Show Rate % - DIVIDE([Total No Show Bookings], [Total Bookings], 0)<br>
   Total Checked Out - CALCULATE([Total Bookings], fact_bookings[booking_status] = "Checked Out")<br>
   Total Cancelled Bookings - CALCULATE([Total Bookings], fact_bookings[booking_status] = "Cancelled")<br>

**5. Create Dashboard:**

   ![Report](https://github.com/VarunWayakole/Hackathon-2.0/assets/91410941/648f61b2-a493-4e64-8a48-b6b8e114683d)

   KPIs:<br>
   Revenue<br>
   Occupancy %<br>
   Average Rating<br>
   RevPar (Revenue Per Available Room)<br>
   ADR (Average Daily Rate)<br>
   DSR (Daily Sellable Rooms)<br>

   Visuals:<br>
   Revenue by City - Clustered Bar Chart<br>
   Occupancy by City<br>
   Weekly Trend by Revenue & Average Rating<br>
   Booking % by Platform<br>
   Occupancy % by Day Type - Donut Chart<br>
   Matrix (Property Name, Revenue, Average Rating, Occupancy %, Cancellation %, Total Capacity)<br>

   Slicers:<br>
   Property Name<br>
   City<br>
   Booking Status<br>
   Platform<br>
   Month<br>
   Week Number<br>
