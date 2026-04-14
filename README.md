# Cost of Living & Savings Dashboard

This project is a data visualization assignment exploring **how far a typical paycheck can stretch across different countries**.

Using a synthetic cost-of-living dataset and Tableau, the project focuses on **where your after-tax income actually goes** – housing, taxes, savings, and other essentials – and how that affects people’s ability to save.

---

## 1. Motivation & Research Question

**Audience:**  
Students and young professionals who are thinking about **which country to live or work in**.

**Core question:**  
> Given income, taxes, and basic living costs, in which countries does a typical person keep the most money **after paying for essentials**, and how has that changed over time?

Instead of just comparing “who has the highest salary,” this project compares countries on:

- After-tax income (take-home pay)  
- Share of take-home pay spent on **housing**  
- Share of take-home pay going into **savings**  
- A simple “**net savings room**” metric (savings minus housing burden)  
- A **savings-to-spending ratio** (“for every \$1 spent, how much is saved?”)

---

## 2. Data

The project uses a synthetic cost-of-living dataset (Kaggle-style) with the following base features:

- `Country`  
- `Year`  
- `Region`  
- `Average_Monthly_Income`  
- `Cost_of_Living` (overall index)  
- `Tax_Rate` (as % of income)  
- `Housing_Cost_Percentage`  
- `Savings_Percentage`  
- `Healthcare_Cost_Percentage`  
- `Education_Cost_Percentage`  
- `Transportation_Cost_Percentage`

These are stored in:

- `data/raw/Original data.csv`  *(path may differ depending on your setup)*

A preprocessing script generates a **processed dataset** with additional, more interpretable metrics for Tableau.

---

## 3. Derived Metrics

All transformations are implemented in the Python script (see below). Key derived features:

### 3.1 TakeHome (after-tax income)

Amount of income remaining after tax:

\[
\text{TakeHome} = \text{Average\_Monthly\_Income} \times \left(1 - \frac{\text{Tax\_Rate}}{100}\right)
\]

### 3.2 Housing_Share_TakeHome_Percent

Percentage of **after-tax (net)** income spent on housing:

\[
\text{Housing\_Share\_TakeHome\_Percent}
= \frac{\text{Housing\_Cost\_Percentage}}{100 - \text{Tax\_Rate}} \times 100
\]

Example: a value of `45` means **45% of net income goes to housing**.

### 3.3 Savings_Share_TakeHome_Percent

Percentage of **after-tax income** going into savings:

\[
\text{Savings\_Share\_TakeHome\_Percent}
= \frac{\text{Savings\_Percentage}}{100 - \text{Tax\_Rate}} \times 100
\]

### 3.4 Net_Savings_Room_Percent

“Room to save” after paying for housing, in percentage points of net income:

\[
\text{Net\_Savings\_Room\_Percent}
= \text{Savings\_Share\_TakeHome\_Percent}
- \text{Housing\_Share\_TakeHome\_Percent}
\]

Positive values mean a larger share of net income goes into savings than into housing.

### 3.5 Other_Essentials_Percentage

Residual percentage of income going to other essentials:

\[
\text{Other\_Essentials\_Percentage} =
100 - (\text{Tax\_Rate}
+ \text{Housing\_Cost\_Percentage}
+ \text{Savings\_Percentage}
+ \text{Healthcare\_Cost\_Percentage}
+ \text{Education\_Cost\_Percentage}
+ \text{Transportation\_Cost\_Percentage})
\]

### 3.6 Savings_to_Spending_Ratio

Savings vs spending, based on **gross** income:

\[
\text{Savings\_to\_Spending\_Ratio} =
\frac{\text{Savings\_Percentage}}{100 - \text{Savings\_Percentage}}
\]

Interpretation: a value of `0.25` means **you save \$0.25 for every \$1 you spend** (before tax).

### 3.7 Savings_to_Spending_Ratio_Net
...
### 4 UI display and URL
The dashboard link is shown as follow: https://public.tableau.com/app/profile/lai.bao/viz/CostofLivingAnalysis_17639960856360/Dashboard1                             <img width="1285" height="722" alt="image" src="https://github.com/user-attachments/assets/7344667e-e2d3-4d6a-aaa1-2f8523ff85cc" />

