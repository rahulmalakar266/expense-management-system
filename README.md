# Expense Management System

A full-stack **Expense Tracking System** built with **Streamlit**, **FastAPI**, **MySQL**, and **Pandas**.  
The project allows users to add or update daily expenses and view category-wise analytics for a selected date range.

---

## Project Overview

Managing daily expenses manually can be difficult and time-consuming. This project solves that problem by providing a simple web-based expense management system where users can:

- Add expenses for a selected date
- Update existing expenses
- Categorize expenses
- Store expense records in a MySQL database
- View analytics by category
- See percentage-wise expense breakdown using charts and tables

---

## Features

### Add / Update Expenses
- Select a date
- Add up to multiple expense entries
- Enter amount, category, and notes
- Update existing records for the selected date
- Save data through FastAPI backend

### Expense Analytics
- Select start date and end date
- Get category-wise total spending
- View percentage contribution of each category
- Display analytics using Streamlit bar chart and table

### Backend API
- FastAPI-based backend
- REST API endpoints for expense operations
- Pydantic models for request validation
- MySQL integration for persistent storage

### Database
- MySQL database named `expense_manager`
- Table: `expenses`
- Stores expense date, amount, category, and notes

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Streamlit |
| Backend | FastAPI |
| Database | MySQL |
| Data Processing | Pandas |
| API Requests | Requests |
| Server | Uvicorn |
| Testing | Pytest |
| Language | Python |

---

## Project Structure

```text
expense-management-system/
│
├── app.py                    # Main Streamlit application
├── add_update_ui.py           # Add/update expense UI
├── analytics_ui.py            # Analytics dashboard UI
├── server.py                  # FastAPI backend server
├── db_helper.py               # MySQL database helper functions
├── expense_db_creation.sql    # Database and table creation script
├── requirements.txt           # Python dependencies
├── test_db_helper.py          # Test cases for database helper functions
├── logging_setup.py           # Logging configuration
└── README.md                  # Project documentation
```

---

## Database Schema

```sql
CREATE TABLE expenses (
    id INT NOT NULL AUTO_INCREMENT,
    expense_date DATE NOT NULL,
    amount FLOAT NOT NULL,
    category VARCHAR(255) NOT NULL,
    notes TEXT,
    PRIMARY KEY (id)
);
```

---

## API Endpoints

### 1. Get Expenses by Date

```http
GET /expenses/{expense_date}
```

Example:

```http
GET /expenses/2024-08-01
```

Returns all expenses for the selected date.

---

### 2. Add or Update Expenses

```http
POST /expenses/{expense_date}
```

Example request body:

```json
[
  {
    "amount": 300,
    "category": "Food",
    "notes": "Groceries"
  },
  {
    "amount": 1200,
    "category": "Rent",
    "notes": "Monthly rent payment"
  }
]
```

---

### 3. Get Analytics

```http
POST /analytics/
```

Example request body:

```json
{
  "start_date": "2024-08-01",
  "end_date": "2024-08-05"
}
```

Example response:

```json
{
  "Food": {
    "total": 600,
    "percentage": 25.0
  },
  "Rent": {
    "total": 1200,
    "percentage": 50.0
  }
}
```

---

## Installation and Setup

### 1. Clone the Repository

```bash
git clone https://github.com/rahulmalakar266/expense-management-system.git
cd expense-management-system
```

---

### 2. Create a Virtual Environment

For macOS/Linux:

```bash
python3 -m venv venv
source venv/bin/activate
```

For Windows:

```bash
python -m venv venv
venv\Scripts\activate
```

---

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

Recommended `requirements.txt` format:

```txt
streamlit==1.35.0
fastapi==0.112.2
pydantic==1.10.9
uvicorn==0.30.6
mysql-connector-python==8.0.33
pandas==2.0.2
requests==2.31.0
pytest==8.3.2
```

---

### 4. Set Up MySQL Database

Login to MySQL:

```bash
mysql -u root -p
```

Run the SQL file:

```bash
source expense_db_creation.sql;
```

Or run directly from terminal:

```bash
mysql -u root -p < expense_db_creation.sql
```

---

### 5. Update Database Credentials

In `db_helper.py`, update your MySQL username and password if needed:

```python
connection = mysql.connector.connect(
    host="localhost",
    user="root",
    password="root",
    database="expense_manager"
)
```

---

## How to Run the Project

### 1. Start the FastAPI Backend

```bash
uvicorn server:app --reload
```

Backend will run at:

```text
http://localhost:8000
```

FastAPI documentation:

```text
http://localhost:8000/docs
```

---

### 2. Start the Streamlit Frontend

Open a new terminal and run:

```bash
streamlit run app.py
```

Streamlit app will open in your browser.

---

## How the Application Works

1. The user opens the Streamlit frontend.
2. The frontend sends API requests to the FastAPI backend.
3. The FastAPI backend performs database operations using `db_helper.py`.
4. MySQL stores and retrieves expense data.
5. The analytics page calculates total spending and percentage breakdown by category.
6. Streamlit displays the results using charts and tables.

---

## Sample Expense Categories

The application currently supports the following categories:

- Rent
- Food
- Shopping
- Entertainment
- Other

---

## Testing

Run tests using:

```bash
pytest
```

Note: Make sure the MySQL database is running and test data exists before running database-related tests.

---

## Future Improvements

- Add user login and authentication
- Add monthly budget tracking
- Add downloadable expense reports
- Add pie charts and monthly trend charts
- Add edit/delete option for individual expenses
- Add deployment using Docker
- Add environment variables for database credentials

---

## Author

**Rahul Malakar**  
GitHub: [rahulmalakar266](https://github.com/rahulmalakar266)

---

## License

This project is open-source and available for learning and portfolio purposes.

