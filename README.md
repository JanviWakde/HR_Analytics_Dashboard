# HR_Analytics_Dashboard

An interactive Power BI dashboard analyzing workforce, compensation, performance, attrition, and satisfaction data for a mid-size organization, built around few business questions across different categories.

## Project Overview
This project uses monthly HR data across three fact/dimension tables to answer questions HR leadership would realistically ask — from basic headcount and cost tracking to attrition drivers and performance-vs-cost tradeoffs. The dashboard is built as a single page, combining KPI cards, department-level breakdowns, and trend visuals across workforce, compensation, performance, attrition, and satisfaction so every key metric is visible at a glance without page-switching.

## Data Model
### Tables:
Employee — EmployeeID, Gender, Age, EducationLevel, DepartmentID, JobRole, HireYear, EmploymentType
Department — DepartmentID, DepartmentName, Region, CostCenter
HR_Monthly — one row per employee per month: BaseSalary, Bonus, OvertimeHours, AbsenteeismDays, PerformanceRating, TrainingHours, AttritionFlag, WorkLifeBalanceScore, JobSatisfactionScore

### Relationships: 
star schema — HR_Monthly many-to-one with both Employee and Department on their respective IDs.

Data quirk worth noting: not every employee has a row in every month — dataset coverage thins out for employees whose most recent record predates the overall latest month in the data. This meant a naive "employees active in the latest calendar month" measure undercounted headcount significantly. The fix was to evaluate each employee's own most recent record rather than filtering to one global latest month — a per-employee ALLEXCEPT-based DAX pattern rather than a simple date filter. Documented as a decision, not hidden.

## Key DAX Measures
Active Employees =
CALCULATE(
    DISTINCTCOUNT(Fact_HR_Monthly[EmployeeID]),
    FILTER(
        VALUES(Fact_HR_Monthly[EmployeeID]),
        VAR CurrentEmp = Fact_HR_Monthly[EmployeeID]
        VAR LastMonthForEmp =
            CALCULATE(
                MAX(Fact_HR_Monthly[StartOfMonth]),
                ALLEXCEPT(Fact_HR_Monthly, Fact_HR_Monthly[EmployeeID])
            )
        VAR LastFlag =
            CALCULATE(
                MAX(Fact_HR_Monthly[AttritionFlag]),
                Fact_HR_Monthly[StartOfMonth] = LastMonthForEmp,
                ALLEXCEPT(Fact_HR_Monthly, Fact_HR_Monthly[EmployeeID])
            )
        RETURN LastFlag = 0
    )
)

Attrition Rate =
DIVIDE(
    CALCULATE(DISTINCTCOUNT(Fact_HR_Monthly[EmployeeID]), Fact_HR_Monthly[AttritionFlag] = 1),
    DISTINCTCOUNT(Fact_HR_Monthly[EmployeeID])
)

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
