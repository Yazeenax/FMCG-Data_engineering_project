🚀 FMCG Data Engineering Pipeline
End-to-end FMCG Data Engineering project built using AWS S3, Databricks, PySpark, Delta Lake, and SQL.

📌 Project Overview
This project demonstrates a complete modern data engineering workflow:

Historical Data Backfill
Incremental Data Loading
Medallion Architecture (Bronze → Silver → Gold)
Dimension & Fact Data Processing
Databricks Jobs & Workflows
Delta Lake Storage
Executive BI Dashboard
🛠️ Technology Stack
AWS S3
Databricks
PySpark
Delta Lake
SQL
GitHub
🏗️ Architecture
S3 Landing Zone
       │
       ▼
 Bronze Layer
       │
       ▼
 Silver Layer
       │
       ▼
  Gold Layer
       │
       ▼
 Databricks Dashboard
📊 Executive Dashboard
Key Business Metrics
Total Revenue
Total Quantity Sold
Unique Customers
Average Selling Price
Business Insights
Revenue by Channel
Monthly Revenue Trend
Top Products by Revenue
Top Customers by Revenue
Product Price vs Quantity Analysis
Dashboard Preview
Dashboard

⚙️ Data Pipeline Components
Dimension Processing
Customer Dimension
Product Dimension
Pricing Dimension
Fact Processing
Incremental Orders Fact Load
Watermark-Based Processing
Automated Workflow Execution
📂 Repository Structure
FMCG-Data_engineering_project
│
├── consolidated_pipeline/
│
├── dashboard/
│
├── sample_data/
│
├── screenshots/
│   └── fmcg-dashboard.png
│
└── README.md
✅ Key Features
Incremental Loading
Historical Backfill
Delta Lake Integration
Medallion Architecture
Automated Databricks Workflows
Executive BI Dashboard

👨‍💻 Author
Yazeen

GitHub: https://github.com/Yazeenax

⭐ If you found this project useful, consider starring the repository.
