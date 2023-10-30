# Worker-Rate-and-Matching-Time
This query serves the purpose of examining worker rates and the duration it takes to confirm bookings across different worker roles. It achieves this by combining data from multiple tables, applying specific filters, and performing time-related calculations to offer valuable insights into the booking process. 
This query was developed during my tenure at an on-demand staffing agency in London, which facilitated job placements through a mobile app available on both Android and iOS platforms.

The provided SQL query, titled "Worker Rate and Matching Time," is used to extract information about workers' roles, company names, booking IDs, hourly rates, and the time it takes to confirm bookings. Here's a step-by-step explanation of the query:

**Title: Worker Rate and Matching Time**

1. **Common Table Expression (CTE)**: 
   - The query starts with a CTE named `time_frame`, which calculates the timestamp for the start of the current week minus one week. This time frame is used for filtering data.

2. **Main Query**:
   - The main part of the query selects various columns:
      - It uses a `CASE` statement to assign human-readable role names based on the values in the `hh.type` column.
      - It retrieves the `company_name` from the `client_client` table, `Booking_id` from the `booking_booking` table, and `freelancer_pay_per_hour` as the rate.
      - It calculates the time it takes to confirm a booking in two formats: `time_to_confirm` in hours and minutes and `days_included` in days, hours, and minutes.
   
3. **Table Joins**:
   - The query performs several joins to retrieve the necessary data:
     - It joins the `hospitality_hospitalityrole` table (`hh`) with the `freelancer_freelancer` table (`ff`) based on `freelancer_id`.
     - It connects the `booking_booking` table (`bb`) to the `job_jobrequest` table (`jj`) through the `freelancer_id` and `jobrequest_id`.
     - It links the `freelancer_freelancer` table (`ff`) with the `hospitality_hospitalityrole` table (`hh`) again.
     - It joins the `client_client` table (`cc`) with the `job_jobrequest` table (`jj`) based on the `client_id`.

4. **Filters**:
   - The query applies several filters:
     - It filters bookings by a specific date (`jj.date >= '03-29-2021'`).
     - It further narrows down the results to only include bookings within the current week based on the `time_frame` CTE.
     - It filters bookings by their status (`bb.status IN ('OK','UN','NS','CA')`), excluding certain statuses.
     - It excludes bookings with a client total cost of '0' (`bb.client_total_cost != '0'`).

5. **Grouping**:
   - The results are grouped by several columns, identified by their numerical positions in the `GROUP BY` clause: `1` (Role), `2` (Company Name), `3` (Booking ID), `4` (Rate), and `5` (Time to Confirm).

In summary, this query is used to analyze worker rates and the time it takes to confirm bookings for various worker roles. It joins multiple tables, applies filters, and calculates time-related metrics to provide insights into the booking process.
