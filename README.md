
# Supermarket Sales Analysis

> Exploratory data analysis and sales prediction on a 1,000-transaction supermarket dataset using Python, Pandas, Seaborn and scikit-learn.

![Python](https://img.shields.io/badge/python-3.x-blue)
![Notebook](https://img.shields.io/badge/Jupyter-Notebook-orange)
![Status](https://img.shields.io/badge/status-complete-brightgreen)

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Dataset Guide](#2-dataset-guide)
3. [Requirements](#3-requirements)
4. [Installation](#4-installation)
5. [How to Run](#5-how-to-run)
6. [Workflow Walkthrough](#6-workflow-walkthrough)
7. [Key Findings](#7-key-findings)
8. [Machine Learning Results](#8-machine-learning-results)
9. [Project Structure](#9-project-structure)
10. [Troubleshooting](#10-troubleshooting)
11. [Future Improvements](#11-future-improvements)
12. [Author](#12-author)

---

## 1. Introduction

This project analyzes supermarket transaction data to understand **what sells, where, to whom, and how customers pay**, and then builds regression models to **predict the sales value of a transaction**.

The whole project lives in one notebook: `Supermarket_Sales_Analysis.ipynb`.

**What you will learn from it**
- How to clean and inspect a retail dataset
- How to explore sales by product line, branch, customer type and payment method
- How to build, compare and evaluate regression models in a scikit-learn pipeline

---

## 2. Dataset Guide

The dataset has **1,000 rows and 17 columns**, with **no missing values and no duplicate rows**.

| Column | Type | Description |
|--------|------|-------------|
| `Invoice ID` | text | Unique invoice number |
| `Branch` | text | Store branch (Alex, Giza, Cairo) |
| `City` | text | City of the store |
| `Customer type` | text | Member or Normal |
| `Gender` | text | Customer gender |
| `Product line` | text | Product category (6 categories) |
| `Unit price` | number | Price per unit (10.08 to 99.96) |
| `Quantity` | number | Units bought (1 to 10) |
| `Tax 5%` | number | 5% tax on the purchase |
| `Sales` | number | Total amount including tax |
| `Date` | date | Purchase date (converted to datetime in the notebook) |
| `Time` | text | Purchase time |
| `Payment` | text | Cash, Ewallet or Credit card |
| `cogs` | number | Cost of goods sold |
| `gross margin percentage` | number | Constant value (4.76) for every row |
| `gross income` | number | Income after cost of goods |
| `Rating` | number | Customer rating (4.0 to 10.0) |

---

## 3. Requirements

| Requirement | Notes |
|-------------|-------|
| Python 3.x | Check with `python --version` |
| Jupyter Notebook or JupyterLab | To open the `.ipynb` file |
| pandas, numpy | Data handling |
| matplotlib, seaborn | Charts |
| scikit-learn | Models and evaluation |

---

## 4. Installation

### Step 1: Clone the repository

```bash
git clone https://github.com/your-username/your-repo.git
cd your-repo
```

### Step 2: Install dependencies

```bash
pip install pandas numpy matplotlib seaborn scikit-learn jupyter
```

### Step 3: Add the dataset

Place `SuperMarket Analysis.csv` in the project folder (or any folder you prefer).

---

## 5. How to Run

1. Start Jupyter:
   ```bash
   jupyter notebook
   ```
2. Open `Supermarket_Sales_Analysis.ipynb`.
3. **Update the file path** in the data loading cell. The notebook currently reads from a local Windows path:
   ```python
   df = pd.read_csv(r"C:\Users\Shyam A\Downloads\archive (6)\SuperMarket Analysis.csv")
   ```
   Change it to where your CSV is, for example:
   ```python
   df = pd.read_csv("SuperMarket Analysis.csv")
   ```
4. Run all cells from top to bottom (**Kernel > Restart & Run All**).

---

## 6. Workflow Walkthrough

| Step | What happens |
|------|--------------|
| 1. Load data | Import libraries and read the CSV |
| 2. Inspect | `head()`, `shape`, `info()`, `describe()` |
| 3. Clean | Check nulls and duplicates, convert `Date` to datetime |
| 4. Explore | Sales by product line, branch, customer type, payment method, and daily trend |
| 5. Correlation | Heatmap of numerical features |
| 6. Prepare features | One-hot encode categorical columns, pass numerical columns through |
| 7. Split | 80% train / 20% test (`random_state=42`) |
| 8. Model | Train Linear Regression and Decision Tree Regressor |
| 9. Evaluate | Compare MAE, RMSE and R², plot Actual vs Predicted |

**Features used for prediction:** Branch, City, Customer type, Gender, Product line, Unit price, Quantity, Payment, Rating.
**Target:** `Sales`.

---

## 7. Key Findings

**Overall:** total sales are **322,966.75**, with an average of **322.97** per transaction.

**Sales by product line**

| Product line | Total sales |
|--------------|-------------|
| Food and beverages | 56,144.84 |
| Sports and travel | 55,122.83 |
| Electronic accessories | 54,337.53 |
| Fashion accessories | 54,305.90 |
| Home and lifestyle | 53,861.91 |
| Health and beauty | 49,193.74 |

**Sales by branch:** Giza leads with 110,568.71, followed by Alex (106,200.37) and Cairo (106,197.67).

**Sales by customer type:** Members account for 189,694.76 versus 133,271.99 for Normal customers.

**Payment methods:** transaction counts are close (Ewallet 345, Cash 344, Credit card 311). Cash brings in the most sales (112,206.57), and Credit card the least (100,767.07).

**Correlation**
- `Sales`, `Tax 5%`, `cogs` and `gross income` are perfectly correlated (1.00).
- `Quantity` (0.71) and `Unit price` (0.63) are the strongest drivers of `Sales`.
- `Rating` has almost no correlation with sales (about -0.04).
- `gross margin percentage` is constant, so it carries no information.

---

## 8. Machine Learning Results

| Model | MAE | RMSE | R² |
|-------|-----|------|----|
| Linear Regression | 59.38 | 79.90 | 0.9019 |
| Decision Tree Regression | 8.49 | 13.13 | 0.9974 |

**Best model:** Decision Tree Regression.

> **Note:** `Sales` is calculated as `Unit price × Quantity × 1.05`, so it is almost a direct formula of two input features. The very high R² reflects that relationship and may not carry over to forecasting real, unseen sales. For a more realistic prediction task, consider predicting future daily or weekly sales instead.

---

## 9. Project Structure

```
your-repo/
├── Supermarket_Sales_Analysis.ipynb   # Full analysis and models
├── SuperMarket Analysis.csv           # Dataset (add yourself)
└── README.md                          # This manual
```

---

## 10. Troubleshooting

| Problem | Cause | Solution |
|---------|-------|----------|
| `FileNotFoundError` on `read_csv` | Path points to the author's computer | Update the path as shown in section 5 |
| `ModuleNotFoundError` | A library is missing | Run the `pip install` command in section 4 |
| Charts do not show | Not running in Jupyter | Use Jupyter Notebook or add `plt.show()` |
| Different results each run | Random split | Keep `random_state=42` |

---

## 11. Future Improvements

- Forecast daily sales using time-series methods
- Try Random Forest or Gradient Boosting (Random Forest is already imported)
- Add cross-validation and hyperparameter tuning
- Build a small dashboard for branch and product comparisons

---

## 12. Author

ADITHYA N T
GitHub: [adithyant24cs-hue](https://github.com/adithyant24cs-hue)

---

