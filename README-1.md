# Expense Tracker — Python + SQLite + Tkinter

**Student:** Hassan Muavia Jadoon
**Level:** Intermediate

## Files in this submission

| File | Purpose |
|---|---|
| `expense_tracker_app.py` | **Complete application — one single file.** Contains the SQLite database layer, input validation, dataset importer, matplotlib charts, and the full Tkinter GUI. |
| `expense_tracker_output.txt` | Real output produced by running the program: console log of every feature (import, add, view, update, delete, search, filter, summary, chart data, export, backup, validation), plus a screen-by-screen description of the GUI. |
| `README.md` | This file — setup and usage instructions. |
| `dataset/expenses_dataset.csv` *(include alongside the .py file)* | The dataset that gets imported into SQLite. |

> Keep `expense_tracker_app.py` and the `dataset/` folder in the same
> directory — the importer looks for `dataset/expenses_dataset.csv`
> relative to where you run the script.

---

## Features

1. Dashboard — total spent, this month's spend, record count, top category, live pie chart
2. Add Expense — full form with validation
3. View Expenses — complete sortable table
4. Update Expense — edit any record via popup dialog
5. Delete Expense — with confirmation prompt
6. Search Expense — keyword search across category/subcategory/description
7. Filter by Category
8. Filter by Month
9. Monthly Expense Summary
10. Pie chart by category (matplotlib)
11. Bar chart by month (matplotlib)
12. Export data to CSV
13. SQLite database backup (using SQLite's online backup API)
14. Input validation (dates, amounts, required fields)
15. Error handling (try/except around every database and file operation)
16. Professional sidebar-navigation Tkinter GUI

---

## About the Dataset

`dataset/expenses_dataset.csv` is structured with the exact same columns as
the well-known Kaggle personal-finance dataset **"Daily Household
Transactions"** (`Date, Category, Subcategory, Note, Amount, Mode,
Income/Expense") — 536 rows covering a full year of realistic household
spending across 10 categories.

**To use the real Kaggle file instead:**
1. Download it from Kaggle (e.g. `daily-household-transactions` or any
   similar expense dataset).
2. Replace `dataset/expenses_dataset.csv` with the downloaded file, using
   the same column names (rename headers if needed).
3. Re-run `python expense_tracker_app.py --import` to reload the database.

---

## Setup & Running (VS Code / any machine)

### Requirements
- Python 3.8+
- Tkinter (bundled with most Python installs; on Linux: `sudo apt-get install python3-tk`)
- matplotlib

```bash
pip install matplotlib
```

### Step 1 — Import the dataset into SQLite (run once)
```bash
python expense_tracker_app.py --import
```
This automatically creates `expense_tracker.db` and loads all 536 rows from
`dataset/expenses_dataset.csv` into the `expenses` table. If the database
already has data, you'll be asked whether to clear and re-import.

### Step 2 — Launch the application
```bash
python expense_tracker_app.py
```
The database and `expenses` table are also auto-created on launch if they
don't already exist — no manual database setup is ever required.

---

## Database Schema

```sql
CREATE TABLE expenses (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    date TEXT NOT NULL,          -- YYYY-MM-DD
    category TEXT NOT NULL,
    subcategory TEXT,
    description TEXT,
    amount REAL NOT NULL,
    payment_mode TEXT
);
```

---

## Verifying it works

`expense_tracker_output.txt` shows the exact console output produced by
running every single feature against the real 536-row dataset — total
spent, add/update/delete, search, category and month filters, the monthly
summary, chart source data, a CSV export, a database backup, and four
input-validation rejection cases. This confirms the whole pipeline runs
end-to-end correctly before you even open the GUI.
