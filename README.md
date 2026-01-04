
---

## 🧱 Project Layers

### 1️⃣ OLTP
- Transactional source system
- Contains raw sales, customer, and product data

### 2️⃣ Staging Area (SA)
- Raw copy of OLTP data
- No business logic
- Used to isolate analytics from OLTP

### 3️⃣ Semantic Layer (Views)
- Business-ready views
- Centralized transformation logic
- Simplifies DWH loading

### 4️⃣ Data Warehouse (DWH)
- Star Schema design
- Optimized for analytical queries

---

## ⭐ Data Warehouse Design

### Dimensions
- **DimCustomer**
- **DimProduct**

### Fact Tables
- **FSales**
- **FReturns**

---

### 📐 DimCustomer
| Column | Description |
|------|------------|
| CustomerKey | Customer identifier |
| Customer | Customer name |
| BusinessType | Customer type |
| CityName | City |
| StateCode | State code (`UNK` if missing) |
| CountryName | Country |
| Continent | Continent |

> 📌 Missing StateCode values are handled using `'UNK'` to maintain data integrity.

---

### 📐 DimProduct
| Column | Description |
|------|------------|
| ProductKey | Product identifier |
| ProductName | Product name |
| CategoryName | Category |
| SubcategoryName | Subcategory |
| Size | Package size |
| Detail | Product details |

---

### 📊 FSales
| Column | Description |
|------|------------|
| OrderDate | Order date |
| SalesOrderNumber | Order ID |
| CustomerKey | FK to DimCustomer |
| ProductKey | FK to DimProduct |
| OrderQuantity | Quantity sold |
| UnitPrice | Unit price |
| UnitCost | Cost |
| DiscountPct | Discount percentage |
| Discount | Discount value |
| NetSales | Net revenue |

---

### 📊 FReturns
| Column | Description |
|------|------------|
| ReturnDate | Return date |
| SalesOrderNumber | Related order |
| CustomerKey | FK to DimCustomer |
| ProductKey | FK to DimProduct |
| ReturnQuantity | Quantity returned |
| ReturnAmount | Financial impact |

---

## 🔁 ETL Process

### Load Strategy
- **Full Load**
- `TRUNCATE + INSERT`
- Managed via stored procedures

### Key Stored Procedures
| Procedure | Description |
|---------|-------------|
| `sploaddimcustomer` | Load customer dimension |
| `sploaddimproduct` | Load product dimension |
| `sploadfactsales` | Load sales fact |
| `sploadfactreturns` | Load returns fact |
| `spLoadHeavyPowerNutritionDWH` | Master ETL orchestration |

---

## 🧪 Data Quality & Error Handling
- NOT NULL constraints on critical columns
- Default business values (`UNK`) for missing attributes
- TRY / CATCH error handling
- Explicit transactions (COMMIT / ROLLBACK)

---

## ⏰ Automation
- SQL Server Agent Job
- Executes master ETL procedure
- Supports daily or hourly scheduling
- Execution monitoring via job history

---

## 📊 Reporting
- Designed for Power BI integration
- Star schema ensures high-performance reporting
- Supports sales, profit, discount, and return analysis

---

## 🚀 Technologies Used
- Microsoft SQL Server
- T-SQL
- SQL Server Agent
- Power BI (Reporting Layer)

---

## 🏆 Key Highlights
✔ Enterprise-ready ETL pipeline  
✔ Clean Star Schema design  
✔ Robust error handling  
✔ Production-level documentation  
✔ Portfolio & interview ready  

---

## 📌 Author
**Mohamed Bahaaeldien**  
Data Analyst / Data Engineer  

---

## 📄 License
This project is for educational and portfolio purposes.
