📊 Power BI Data Import & Transformation
From raw tables to a clean, analysis-ready data model

Show Image Show Image Show Image Show Image

</div>
🎯 Project Overview

In this project I used Power Query Editor in Power BI to import, clean, transform, combine and model sales data across three tables:

🗂️ Table
🧾 List of Orders
📦 Order Details
🎯 Sales Target
📑 Table of Contents
#	Task	#	Task
1️⃣	Data Import	6️⃣	Merging Data
2️⃣	Row Limiting & Data Types	7️⃣	Missing & Duplicate Data
3️⃣	Text Formatting	8️⃣	Sorting & Filtering
4️⃣	Column Creation	9️⃣	Grouping & Aggregating
5️⃣	Conditional Column	🔟	Data Modeling
1. 📥 Data Import

Loaded the source tables into Power Query Editor via Home → Transform data.

Data import

2. ✂️ Row Limiting & Data Types

🔢 Restricted the List of Orders table to the first 500 rows Home → Keep Rows → Keep Top Rows → 500

powerquery
= Table.FirstN(Source, 500)

Keep top 500 rows

📅 Set the Order Date column to the Date data type

Order Date data type

💰 Changed the Amount and Target columns to Fixed Decimal Number

Fixed decimal number

3. 🔤 Text Formatting

✍️ Formatted Customer Name to proper case for consistent capitalization.

Proper case

4. 🧱 Column Creation

📍 Location – merged the City and State columns in the format City, State

<img src="images/06-location-column.png" alt="Location column" width="220">

📈 Profit Margin – custom column calculated as Profit / Amount (shown as a percentage)

powerquery
= [Profit] / [Amount]
<img src="images/07-profit-margin.png" alt="Profit Margin column" width="160">
5. 🚦 Conditional Column

Added a Profit Status column:

Condition	Result
Profit < 0	🔴 Loss
Profit = 0	🟡 Break-Even
Profit > 0	🟢 Profit
<img src="images/08-profit-status.png" alt="Profit Status column" width="150">
6. 🔗 Merging Data (Joins)

Merged List of Orders and Order Details on Order ID and named the output table Orders Data.

Merge queries

7. 🧹 Handling Missing & Duplicate Data
🔍 Identified missing values across all tables
🛠️ Applied suitable strategies:
♻️ Replacing missing values
🗑️ Removing records
📌 Retaining nulls with justification
👯 Identified duplicate rows and handled them based on business logic

Missing and duplicate data

8. 🔃 Sorting and Filtering Data

⬇️ Sorted Orders Data by Order Date in descending order

Sort by Order Date

🗺️ Filtered orders for a specific state (e.g., Tamil Nadu)

Filter by state

9. 🧮 Grouping and Aggregating Data

Duplicated the Order Details table and calculated:

🔢 Count of Order ID

Count of Order ID

📊 Average Profit by Category

Average profit by category

💵 Total Amount by Sub-Category

Total amount by sub-category

Duplicated the Sales Target table and aggregated the total Target by month of order date.

Target by month

10. 🕸️ Data Modeling
🔗 Relationship	🔑 Key
List of Orders ↔ Order Details	Order ID
Order Details ↔ Sales Target	Category

List of Orders ↔ Order Details

Relationship: List of Orders and Order Details

Order Details ↔ Sales Target

Relationship: Order Details and Sales Target

✅ Verified in Manage Relationships that both relationships are active and correctly defined.

🧰 Skills Demonstrated
⚙️ Power Query transformations
🧬 Custom & conditional columns
🔗 Merging queries (joins)
🧼 Data cleaning (nulls & duplicates)
🧮 Grouping & aggregation
🕸️ Data modeling & relationships
