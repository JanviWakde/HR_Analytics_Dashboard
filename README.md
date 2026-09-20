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
- Out of 394 total employees ever recorded, 339 are currently active; overall attrition rate is 41.1%.
- Attrition varies meaningfully by department — highest in Marketing (21.5%) and HR (19.1%), lowest in IT (13.0%) and Sales (13.9%).
- No two departments share nearly the same rate, so attrition drivers are likely department-specific rather than company-wide.

### Compensation
- Total workforce compensation cost is ₹140M (base salary + bonus).
- Average monthly salary is fairly tight across departments (₹70K–₹74K), with HR paying highest on average (~₹74K) and Finance lowest (~₹70K) — a narrower spread than the attrition-rate spread, suggesting pay alone doesn't explain attrition differences.

### Performance & Productivity
- Company-wide average performance rating is 3.46/5.
