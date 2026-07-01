# Tableau Assignment Solutions

🌟 **[Click here to view the Interactive Tableau Dashboard on Tableau Public!](https://public.tableau.com/shared/YWTBC5ZPK)** 🌟

This repository contains the completed Tableau workbook (`tableau assignment .twbx`) which addresses all 7 assignments. Below is a detailed explanation of the solution for each assignment.

## Assignment 1: Charts & Quick Table Calculations
**Goal**: Create a table with category, sub-category (rows) and region (columns) showing total sales, total profit, grand total, and percent of pane total sorted by sum of sales descending.

**Explanation**:
- **Rows**: Added `Category` and `Sub-Category`.
- **Columns**: Added `Region` and `Measure Names`.
- **Marks/Values**: Added `Sum(Sales)` and `Sum(Profit)` to the text label.
- **Table Calculations**: Applied a Quick Table Calculation for "Percent of Total" to Sales/Profit, computed using "Pane (Down)" to get the percent of pane total.
- **Totals**: Enabled Column Grand Totals from the Analysis > Totals menu.
- **Sorting**: Sorted the `Sub-Category` field by `Sum(Sales)` in descending order.

## Assignment 2: Data Combining Techniques & Filtering
**Goal**: From Netflix Titles dataset, use Inner Joins to identify the actor/actress with the highest number of appearances in Sports Movies, and list their movies.

**Explanation**:
- **Data Source**: Brought in the Netflix Titles dataset. Connected multiple tables using Inner Joins on the appropriate ID fields.
- **Filtering**: Added a filter on the "Listed In" or "Genres" field to include only "Sports Movies".
- **View**: Added the `Cast` / Actor name to Rows, and `Count(Show ID)` to Columns. Sorted descending to find the top actor.
- **Drill-down**: Added `Title` to the Rows to display the specific movies they starred in. 

## Assignment 3: LODs & Histogram
**Goal**: Create a histogram of customer count based on order frequency.

**Explanation**:
- **Calculated Field (LOD)**: Created a Fixed LOD expression to calculate the number of orders per customer: `{FIXED [Customer Name] : COUNTD([Order ID])}`.
- **Bins / Dimensions**: Converted this new measure to a Dimension (or created bins from it) to serve as the x-axis (Order Frequency).
- **View**: Placed the LOD dimension on Columns and `COUNTD([Customer Name])` on Rows (y-axis) to build the histogram showing how many customers fall into each order frequency bracket.

## Assignment 4: Sets
**Goal**: Create a pie chart showing Top 50 customers vs Other customers with respect to sum of sales.

**Explanation**:
- **Set Creation**: Created a Set on `Customer Name` based on Top 50 by `Sum(Sales)`.
- **Calculated Field**: Created a field to label the set: `IF [Top 50 Customers Set] THEN "Top 50 Customers" ELSE "Other Customers" END`.
- **View**: Chose a Pie Chart mark type. Placed the calculated field on Color and `Sum(Sales)` on Angle. Added labels to show the proportion.

## Assignment 5: Custom Visual: KPI Card & Table Calculations
**Goal**: KPI card for current year total profit, percentage growth from previous year (with up/down arrows), and a line chart of monthly profit trends.

**Explanation**:
- **Current Year Filter/Calculation**: Filtered data to the current/last year of the dataset.
- **Growth Calculation**: Used a Quick Table Calculation for "Percent Difference" on `Sum(Profit)` relative to the previous year. 
- **Custom Formatting**: Formatted the growth percentage field using custom number formatting: `▲ 0.00%; ▼ -0.00%` (using the requested arrows and signs) and colored it green for positive, red for negative.
- **Trend Line**: Placed `MONTH(Order Date)` on Columns and `Sum(Profit)` on Rows as a line chart, placing it below the main KPI number.

## Assignment 6: Parameters & Groups
**Goal**: Parameter to toggle view by Region, Category, or Sub-category. Group specific brands (Acco, 3M, Samsung, Apple, Xerox) vs Others, and show average discount percentage.

**Explanation**:
- **Parameter**: Created a parameter "View by" (String list: Region, Category, Sub-Category).
- **Calculated Field**: Created a field "Dynamic Dimension": 
  `CASE [View by] WHEN 'Region' THEN [Region] WHEN 'Category' THEN [Category] WHEN 'Sub-Category' THEN [Sub-Category] END`.
- **View 1 (Dynamic Chart)**: Placed "Dynamic Dimension" on Rows and `Sum(Sales)` on Columns. Inserted the parameter into the title.
- **Grouping**: Selected the `Product Name` or `Manufacturer` field, and grouped 'Acco', '3M', 'Samsung', 'Apple', and 'Xerox' together. Checked "Include Other" for the rest.
- **View 2 (Group Chart)**: Placed the Group on Rows and `AVG(Discount)` on Columns.

## Assignment 7: Dashboard
**Goal**: Divide dashboard into left (controls/filters) and right (6 charts + 3 KPIs). Dynamic metric selection parameter. Filter actions.

**Explanation**:
- **Layout**: Used horizontal and vertical layout containers to split the dashboard into a left pane (logo, parameter, filters) and right pane (visualizations).
- **Metric Parameter**: Created a string parameter "Metric" (Sales, Profit, # Orders). Created a dynamic measure calculated field based on it:
  `CASE [Metric] WHEN 'Sales' THEN [Sales] WHEN 'Profit' THEN [Profit] WHEN '# Orders' THEN [Number of Records/Orders] END`.
- **Visualizations**: Swapped out static measures with the dynamic measure in all 6 charts and 3 KPI cards. Updated titles to dynamically include the `[Metric]` parameter.
- **Top 5 Context Filter**: Created a Top 5 Product set/filter based on the dynamic measure. Added the Region and Year filters to "Context" so the Top 5 computes *after* filtering. 
- **Show/Hide Filter**: Used a floating layout container for the filters with a "Show/Hide Button", setting the custom icons provided for the button states.
- **Filter Action**: Set up a Dashboard Action (Filter) where clicking on the Category chart filters all other charts and KPIs on the dashboard.
- **URL Action**: Added an image object for the logo with a URL link pointing to the published Tableau Public dashboard.
