
---

# 📊 Demographic Data Analyzer

This project analyzes census demographic data using **Pandas** in Python.
The dataset (`adult_data.csv`) includes information about people’s **age, race, education, occupation, working hours, and income level**.

The goal is to answer demographic questions such as:

* What’s the average age of men?
* Which country has the highesta percentage of high earners?
* What jobs are most common among rich people in India?

---
🧩 Example Mini Dataset

Here’s a fake “dataset” in table form:

age	sex	education	hours-per-week	salary	race	native-country	occupation
25	Male	Bachelors	40	>50K	White	United-States	Tech
30	Female	HS-grad	20	<=50K	Black	India	Sales
45	Male	Masters	50	>50K	White	India	Tech
23	Male	HS-grad	15	<=50K	Asian	China	Farming
50	Female	Doctorate	60	>50K	White	India	Exec

## 🚀 Features & Questions Answered

The script (`demographic_analyzer.py`) answers **9 key questions**:

1. **How many people of each race?**
   Uses `value_counts()` to count unique categories in the `race` column.

   > Example: White: 27816, Black: 3124, etc.

2. **What is the average age of men?**
   Filters rows where `sex == 'Male'` and takes the mean of the `age` column.

3. **What percentage of people have a Bachelor's degree?**
   Counts rows where `education == 'Bachelors'`, divides by total rows, and multiplies by 100.

4. **What percentage of people with advanced education (Bachelors, Masters, Doctorate) make >50K?**
   Uses a **Boolean mask** (`isin`) to filter advanced degrees, then checks income with another mask (`salary == '>50K'`).
   Concept: combine conditions with `&` (AND).

5. **What percentage of people without advanced education make >50K?**
   Uses the inverse mask (`~`) to calculate the same for non-advanced degrees.

6. **What is the minimum number of hours worked per week?**
   Uses `.min()` on `hours-per-week`.

7. **Among people working the minimum hours, what % earn >50K?**
   Filters dataset where `hours-per-week == min_value` and checks salary condition.

8. **Which country has the highest % of rich people?**

   * Counts rich people per country (`df[q2]['native-country'].value_counts()`)
   * Divides by total people per country
   * Finds the max percentage.

9. **What is the most popular occupation for >50K earners in India?**
   Filters for `native-country == 'India'` and salary >50K, then uses `value_counts()` on `occupation`.

---

## 💡 Core Concepts

This project demonstrates key **Pandas concepts**:

* **Filtering rows:**

  ```python
  df[df['sex'] == 'Male']
  ```

  → Selects only male rows.

* **Boolean masks (AND/OR/NOT):**

  ```python
  q1 = df['education'].isin(['Bachelors', 'Masters', 'Doctorate'])
  q2 = df['salary'] == '>50K'
  df[q1 & q2]  # advanced education AND rich
  ```

* **Counting categories:**

  ```python
  df['race'].value_counts()
  ```

* **Aggregation (mean, min, percentage):**

  ```python
  df['age'].mean()
  df['hours-per-week'].min()
  (subset.sum() / total.sum()) * 100
  ```

* **Finding top results:**

  ```python
  df['occupation'].value_counts().index[0]
  ```

  → Gets the most common job.

Think of it as SQL-like queries but in Pandas.

---

## 🛠️ Installation

1. Clone the repo:

   ```bash
   git clone https://github.com/your-username/demographic-analyzer.git
   cd demographic-analyzer
   ```

2. Install requirements:

   ```bash
   pip install pandas
   ```

3. Place `adult_data.csv` in the project folder.

---

## ▶️ Usage

Run the analyzer:

```bash
python demographic_analyzer.py
```

Sample output:

```
Number of each race:
 White                 27816
 Black                  3124
 Asian-Pac-Islander     1039
 Amer-Indian-Eskimo      311
 Other                   271
Average age of men: 39.4
Percentage with Bachelors degrees: 16.4%
Percentage with higher education that earn >50K: 46.5%
Percentage without higher education that earn >50K: 17.4%
Min work time: 1 hours/week
Percentage of rich among those who work fewest hours: 10.0%
Country with highest percentage of rich: Iran
Highest percentage of rich people in country: 41.9%
Top occupations in India: Prof-specialty
```

---

## 🧪 Testing

The project comes with **unit tests** (`test_module.py`). Run:

```bash
python -m unittest test_module.py
```

---

## 📂 File Structure

```
.
├── adult_data.csv          # Dataset
├── demographic_analyzer.py # Main analysis script
├── test_module.py          # Unit tests
└── README.md               # Documentation
```

---

## 📖 Credits

* Dataset: [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/adult)
* Project: FreeCodeCamp Data Analysis with Python

---
