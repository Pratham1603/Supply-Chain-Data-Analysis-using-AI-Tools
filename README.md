# 📦 Atliq Mart: AI-Powered Supply Chain Analytics 🚀

### 📖 Project Overview
Atliq Mart, an organic food manufacturer, faced significant customer dissatisfaction due to immature supply chain management and inconsistent inventory levels. This project replaces traditional manual reporting with an **AI-First automated pipeline** to monitor real-time reliability and fulfillment KPIs.

---

### 🏗️ System Architecture
The project utilizes an agentic workflow to move data from unstructured communication (Email) to a cloud data warehouse for AI-assisted analysis.



**Data Flow:** `Email (CSV) ➔ n8n (Automation) ➔ Supabase (PostgreSQL) ➔ Quadratic (AI Spreadsheet)`

---

### 💻 Tech Stack
* **n8n**: Agentic workflow automation to monitor Gmail, extract CSV attachments, and ingest data.
* **Supabase (PostgreSQL)**: Cloud-hosted relational database utilizing a Star Schema for data warehousing.
* **Quadratic**: An AI-powered spreadsheet used to perform Python-based data cleaning and KPI generation.
* **Python (Pandas)**: Used within Quadratic for advanced data merging and transformation.

---

### ⚙️ Data Pipeline & Workflows

#### 📧 1. Automated Ingestion (n8n & Gmail)
The n8n workflow monitors a specific Gmail label (`daily sales`). When an email arrives, the agent:
* Extracts the CSV attachment.
* Converts data to JSON format.
* Standardizes date formats (ISO) for database compatibility.
* Inserts records into the corresponding Supabase Fact tables.



#### 🗄️ 2. Data Modeling (Supabase)
The database follows a **Star Schema** to optimize analytical queries:
* **Fact Tables**: `fact_orders_line`, `fact_aggregate`.
* **Dimension Tables**: `dim_customers`, `dim_products`, `dim_targets_orders`.



#### 📊 3. AI-Assisted Analysis (Quadratic)
Using Quadratic’s AI agent, we generated Python scripts to:
* Create a dynamic `dim_date` table.
* Fetch real-time exchange rates (USD/INR) via API.
* Generate a merged `fact_summary` for high-level reporting.

---

### 📈 Key Supply Chain Metrics
This project tracks essential KPIs to measure delivery reliability:

| Metric | Level | Description |
| :--- | :--- | :--- |
| **LFR (Line Fill Rate)** | Line | % of individual items shipped in full vs. ordered. |
| **VFR (Volume Fill Rate)** | Volume | Total quantity shipped vs. total quantity ordered. |
| **On Time %** | Order | % of orders where 100% of lines arrived by the agreed date. |
| **In Full %** | Order | % of orders where 100% of lines were delivered in requested quantity. |
| **OTIF %** | Order | The "Perfect Order" metric—both On Time and In Full. |

---

### 🚀 How to Run
1. **Database**: Execute the SQL scripts in `/sql/schema.sql` within your Supabase SQL editor.
2. **Automation**: Import the `n8n_workflow.json` into your n8n instance and connect your Gmail/Supabase credentials.
3. **Analysis**: Open the Quadratic file and run the Python cells to refresh the analytical summary.

---
*Project inspired by Codebasics AI Data Analysis series.*