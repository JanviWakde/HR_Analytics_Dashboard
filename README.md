# HR_Analytics_Dashboard

An interactive Power BI dashboard analyzing workforce, compensation, performance, attrition, and satisfaction data for a mid-size organization, built around few business questions across different categories.

## Project Overview
This project uses monthly HR data across three fact/dimension tables to answer questions HR leadership would realistically ask — from basic headcount and cost tracking to attrition drivers and performance-vs-cost tradeoffs. The dashboard is built as a single page, combining KPI cards, department-level breakdowns, and trend visuals across workforce, compensation, performance, attrition, and satisfaction so every key metric is visible at a glance without page-switching.

## Tool used
Power BI desktop app

## Data Model
### Tables:
Employee_Data — EmployeeID, Gender, Age, EducationLevel, DepartmentID, JobRole, HireYear, EmploymentType
Department — DepartmentID, DepartmentName, Region, CostCenter
HR_Monthly — one row per employee per month: BaseSalary, Bonus, OvertimeHours, AbsenteeismDays, PerformanceRating, TrainingHours, AttritionFlag, WorkLifeBalanceScore, JobSatisfactionScore

### Relationships: 
Star schema — HR_Monthly many-to-one with both Employee and Department on their respective IDs.

### Business Questions Covered
## Category	Examples
- Workforce & Headcount:	Active employees, headcount trend over time, department size
- Compensation & Cost:	Total comp cost, avg salary by department, highest-paid roles
- Performance & Productivity:	Performance by department/role, avg performance rating
- Attrition & Retention:	Overall attrition rate, attrition by department
- Satisfaction & Well-Being: Work-life balance by department

## Key Findings

## Headcount & Attrition -
- Out of 394 total employees ever recorded, 339 are currently active; overall attrition rate is 13.96%.
- Attrition varies by department — highest in Customer Support (20.00%) and Finance (16.22%), lowest in Marketing (8.77%) and HR (10.91%).
- Several departments have very similar rates (for example IT 13.95%, Operations 13.64% and Sales 14.29%), and each department has only about 5 to 9 leavers, so department differences are leads to investigate, not proven drivers

### Compensation
- Total workforce compensation cost is ₹140M (base salary + bonus).
- Average monthly salary is fairly tight across departments (₹71K–₹74K), with Operations paying highest on average (~₹74K) and HR and Marketing lowest (~₹71K) — a narrower spread than the attrition-rate spread, suggesting pay alone doesn't explain attrition differences.

### Performance & Productivity
- Company-wide average performance rating is 3.46/5.

