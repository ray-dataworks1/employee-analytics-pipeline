# 🧠 Business Logic: Employees Analytics Engine

## 1. 🎯 Project Goal

The objective of this analytics engine is to empower internal stakeholders at **PulseMetrics**, a fictitious HR analytics platform, with the insights and data infrastructure needed to:
- Understand and improve employee compensation structures
- Comply with legal wage policies
- Create transparent, data-driven performance-based reward systems
- Boost retention through deep analysis of satisfaction, tenure, and management effectiveness

---

## 2. 🧑‍💼 Target Stakeholders

| Role                     | Interest                                                                 |
|--------------------------|--------------------------------------------------------------------------|
| **C-Suite Executives**   | Strategic HR policy, pay equity, retention, PR, DEI metrics              |
| **People Analytics Team**| Operational KPIs, survey analysis, salary modeling, tenure optimization |
| **Department Heads**     | Performance tracking, morale alignment, pay fairness                    |

---

## 3. 🗃️ Key Business Questions & Metrics

| 📊 Question / Metric | 🛠️ Data Source(s) | 💡 Transform Logic |
|----------------------|-------------------|--------------------|
| **Which department has the highest salaries?** | `Employees`, `Departments` | `AVG(salary)` + `GROUP BY department_id` |
| **Create salary bands across departments** | `Employees` | `NTILE()` / quartile `CASE` logic using WFs |
| **Commission structure for Sales** | `Employees`, `Performance_Reviews` | Add derived `commission = base * factor` column (Sales only) |
| **Who earns below UK minimum wage (2025)?** | `Employees` | `WHERE salary / weekly_hours < 11.44` (or your hourly base) |
| **Apply uniform pay changes by performance** | `Performance_Reviews` | `CASE WHEN score = 'High' THEN +7% ...` |
| **Average tenure of engineers** | `Employees` | `DATEDIFF(separation_date, hire_date)` + `AVG()` on Engineering dept |
| **Why is retention low in Legal?** | `Surveys`, `Employees` | Text analytics + exit survey correlation + tenure patterning |

---

## 4. 📦 Core Tables (Modeled in ERD)

- `Employees`
- `Departments`
- `Performance_Reviews`
- `Surveys`
- [Optional: `Salary_Bands`, `Commission_Models`, `Seniority_Levels`]

---

## 5. 🧠 KPIs to Track or Derive

| KPI                             | Description |
|---------------------------------|-------------|
| Average Salary per Department   | For internal equity tracking |
| Salary to Market Ratio          | Derived from survey inputs or external table |
| Quartile Band Classification    | `NTILE(4) OVER (PARTITION BY dept ORDER BY salary)` |
| Tenure (in months or years)     | Derived from hire/separation dates |
| Burnout Score / Retention Risk  | From Surveys |
| Compliance Flag                 | Binary flag for min wage compliance |
| Promotion Readiness             | Optional composite score using salary, tenure, review score |

---

## 6. 🧪 Assumptions & Future Expansions

- Sales commission logic is placeholder — could be modular per region/product line
- Market salary ratios assumed from employee perception — can be replaced with scraped or externally sourced benchmarks
- Text-based survey columns may later feed into NLP pipelines
