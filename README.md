# Streaming Platform Analytics Dashboard

An interactive **Power BI analytics dashboard** designed to turn streaming-activity data into actionable insights on **user engagement, content performance, geographic distribution, package behavior, and regional performance**.

> **Portfolio case study:** from raw streaming activity and data preparation to DAX-driven analysis, interactive dashboard design, and province-level decision support.

---

## Project Overview

Streaming platforms generate large amounts of activity data across users, content, packages, devices, geography, timestamps, and viewing behavior.

This project consolidates that activity into a focused Power BI solution that allows stakeholders to move from a **national overview** to **province-level analysis** without relying on separate manual reports.

The dashboard is designed around one core question:

> **How can streaming activity data be transformed into actionable insight on user engagement, content performance, and regional behavior — from a national overview down to province-level detail?**

---

## Business Problem

The raw streaming dataset contains many attributes, but the information is difficult to interpret when viewed as disconnected fields or exports.

The project addresses three main problems:

### 1. Fragmented Metrics

User, content, package, device, province, and viewing activity exist across many raw attributes, making it difficult to form one consistent view of platform performance.

### 2. No Unified Insight Layer

Stakeholders need one place to understand:

- User base
- Engagement
- Content consumption
- Package distribution
- Geography
- Demographic behavior

### 3. No Easy National-to-Regional Drill-Down

A national dashboard alone does not explain what is happening within a specific province.

The **Detail Province** page provides the regional drill-down needed to move from:

**National Overview → Selected Province → Local Content / Package / Trend Analysis**

---

## Analytical Objectives

The dashboard is built around five analytical questions:

1. **How large is the active user base, and how does activity move over time?**
2. **Which provinces contribute the most users at the national level?**
3. **Which content titles and package tiers drive the most engagement?**
4. **How does user behavior differ across age groups and devices?**
5. **How can a stakeholder move from a national view into one specific province?**

---

## Dashboard Structure

### 1. Dashboard — Executive Overview

Provides the national-level view of platform performance.

Key elements include:

- Total Users
- Total Streaming Hours
- Average Watch Time
- Users Month-over-Month %
- Monthly activity trend
- Users by Province
- Streaming Hours by Content Type
- Users by Package Tier
- Users by Age Group
- Device OS breakdown
- Interactive slicers
- Metric Selector

### 2. Detail Province — Regional Drill-Down

Provides a focused view for a selected province.

Key elements include:

- Province ranking
- Share of national users
- Province-level KPI
- Dominant age group
- Top content type
- Province-level trend
- Package distribution
- Top 5 content by streaming hours
- Dynamic province insight

---

# Dashboard Preview

The dashboard screenshots are available in the `screenshots/` folder.

---

## Key Dashboard Features

### Executive KPI Layer

The dashboard provides headline measures for:

- **Total Users**
- **Total Streaming Hours**
- **Avg Watch Time**
- **Users MoM %**

These KPIs give stakeholders a quick view of platform scale and engagement.

### Dynamic Metric Selector

The monthly trend visual uses a **Power BI field parameter** to switch between:

- Total Users
- Streaming Hours
- Avg Watch Time

This allows multiple engagement perspectives to be explored without duplicating the same chart.

### Geographic Analysis

The national dashboard shows user distribution by province and supports province-level exploration.

This creates a simple flow:

```text
National User Base
        ↓
Province Distribution
        ↓
Selected Province
        ↓
Province Detail
```

### Content Performance

The dashboard compares streaming activity across content types and provides province-level content ranking.

### Package Analysis

Users are distributed across four package tiers, allowing the dashboard to show package composition alongside engagement metrics.

### Demographic & Device Analysis

The dashboard provides breakdowns by:

- Age Group
- Gender
- Device OS

The Device OS metric is accompanied by a data-quality caveat described below.

---

## Data Foundation

The core fact table contains:

- **10,000 viewing-activity rows**
- **20 columns**

One row represents a viewing activity record containing attributes such as:

- User ID
- Province
- City
- Content Name
- Content Type
- Package
- Device
- Age
- Gender
- Watch Duration
- Date

### Core Analytical Tables

The Power BI model uses the following analytical structures:

| Table / Entity | Purpose |
|---|---|
| **Fact_Streaming** | Main viewing-activity fact table |
| **Dim_Calendar** | Date dimension supporting time analysis |
| **Metric Selector** | Field-parameter table for dynamic trend metrics |
| **Ref_ProvinsiIndonesia** | Reference list used to standardize province names |

A supporting query/entity is also present in the model.

---

## Data Preparation

The data preparation workflow is:

```text
Raw Excel Data
      ↓
Power Query
      ↓
Data Cleaning
      ↓
Data Validation
      ↓
Data Model
      ↓
DAX Measures
      ↓
Interactive Power BI Dashboard
```

### Key Power Query transformations

The verified preparation logic includes:

- Parsing timestamps into clean datetime values
- Creating a date-only field
- Converting watch duration from milliseconds into minutes and hours
- Flagging sessions longer than 6 hours as potential outliers
- Standardizing province names against a reference province list
- Classifying province records as Domestic or Overseas / Unmapped

---

## DAX & Power BI Logic

The project uses DAX for KPI calculations, time comparisons, dynamic insight generation, and interactive analytical behavior.

### Important measure categories

- User metrics
- Streaming-hour metrics
- Average watch-time metrics
- Month-over-month calculations
- Province ranking
- Province share
- Dynamic province insights
- Content ranking
- Supporting KPI calculations

### Example: Time Intelligence

The `Users MoM %` calculation is designed to compare the current period against the previous month using the calendar table and date-shifting logic.

Conceptually:

```text
Current Month
      ↓
Previous Month
      ↓
Change
      ↓
MoM %
```

### Example: Dynamic Province Insight

The `Province Insight` measure generates a short narrative based on the selected province, such as:

```text
[Province] contributes [share]% of national users,
is dominated by [age group],
with [content type] as the favorite content type.
```

This demonstrates how DAX can be used not only for numeric calculations but also for **automated business storytelling**.

---

## Data Quality & Limitations

Data quality is treated as part of the analysis rather than hidden.

### 1. Monthly Activity Concentration

The dataset shows that a large proportion of users are concentrated in **May and June 2023**.

This should be interpreted as a **concentration pattern**, not automatically as organic growth, until the data owner confirms the underlying cause.

### 2. Device OS Caveat

The current Android/iOS split should **not be used for an actual device strategy** because the Power Query logic assigns iOS to every fifth record by index.

This is a placeholder transformation rather than observed device-source data.

Therefore:

> **Device OS is retained as a dashboard example, but it should be verified against the original source system before strategic decisions are made.**

### 3. Package Distribution

The four package tiers currently have an equal user count distribution.

Therefore, package tier alone does not provide enough evidence for pricing or upsell recommendations. It should be combined with metrics such as watch hours per package before making commercial decisions.

---

## Key Insights

### 1. Engagement Pattern

The platform activity is highly concentrated in a small part of the observed period.

**Business implication:**  
The apparent monthly pattern should be investigated before being used as a growth KPI.

### 2. Content Consumption

**Channel Live** and **Series** account for the overwhelming majority of streaming hours.

**Business implication:**  
Content investment and licensing priorities should give strong consideration to these two formats.

### 3. Geographic Concentration

**Jakarta, West Java, and East Java** represent the largest combined share of national users.

**Business implication:**  
These provinces provide an important base for retention and acquisition activity, while smaller provinces can be evaluated for targeted expansion opportunities.

### 4. Package Distribution

All four package tiers currently have an equal user distribution.

**Business implication:**  
There is no clear package usage skew from user count alone; engagement by tier should be analyzed before recommending pricing or upsell actions.

### 5. Demographic Core

The **26–35 age group** is the largest user segment.

**Business implication:**  
This segment can be treated as a strong starting point for customer and engagement strategies, while device-specific conclusions should wait for validated device-source data.

---

## Regional Drill-Down Example

The **Detail Province** page demonstrates how a national metric can become a local business story.

Example flow:

```text
National Dashboard
        ↓
Select Province
        ↓
Province Detail
        ↓
Rank / Share / Age / Content / Package
        ↓
Dynamic Province Insight
```

For a selected province, the page can show:

- Rank among provinces
- Share of national users
- Dominant age group
- Top content type
- Top content titles
- Package distribution
- Province trend

This turns the dashboard into a **regional decision-support tool**, rather than a static national report.

---

## Business Recommendations

### Product / Platform Team

- Investigate the May–June activity spike before using the trend as a growth target.
- Validate the Device OS source field before making platform or device-prioritization decisions.
- Establish a recurring data-validation process for decision-facing dashboards.

### Content Team

- Prioritize analysis and investment around **Channel Live** and **Series**, which account for most streaming hours.
- Review the long-tail content catalog to identify titles with weak engagement.

### Marketing / Customer Team

- Prioritize retention and acquisition analysis for the largest user-contributing provinces.
- Use province-level drill-downs to develop more targeted regional campaigns.

### Management

- Combine package usage with streaming hours or other engagement metrics before making package-pricing decisions.
- Use the dashboard as a common analytical layer for national and regional performance discussions.

---

## Decision Framework

The dashboard supports a repeatable decision flow:

```text
User Monitoring
       ↓
Engagement Analysis
       ↓
Content & Package Analysis
       ↓
Regional Drill-Down
       ↓
Business Recommendation
       ↓
Decision Support
```

---

## Technology Stack

- **Microsoft Power BI**
- **DAX**
- **Power Query**
- Power BI Field Parameters
- Interactive Slicers
- Data Validation
- Dynamic Text Insights
- Province-level drill-down

---

## Project Deliverables

Recommended GitHub repository structure:

```text
streaming-platform-powerbi-dashboard/
│
├── README.md
│
├── dashboard/
│   └── Streaming Platform Dashboard.pbix
│
├── report/
│   ├── Streaming Platform Dashboard.pptx
│   └── Streaming Platform Dashboard.pdf
│
└── screenshots/
    ├── dashboard-overview.png
    └── detail-province.png
```

---

## How to Use

### Option 1 — Interactive Dashboard

Open:

```text
dashboard/Streaming Platform Dashboard.pbix
```

using **Power BI Desktop**.

### Option 2 — Case Study Report

Open the PowerPoint/PDF in:

```text
report/
```

This is suitable for recruiters and stakeholders who do not have Power BI Desktop.

### Option 3 — Portfolio Preview

Use the screenshots in:

```text
screenshots/
```

for GitHub and your personal portfolio website.

---

## Portfolio Highlights

This project demonstrates the ability to:

- Translate a business problem into analytical questions
- Prepare and validate activity-level data
- Build a compact Power BI data model
- Develop KPI and time-intelligence measures in DAX
- Build dynamic metric selection using field parameters
- Create province-level drill-down analysis
- Generate dynamic text-based insights
- Identify and communicate data-quality limitations
- Turn descriptive analytics into business recommendations
- Present findings in a stakeholder-friendly format

---

## Data Quality Philosophy

A central principle of this project is:

> **Do not hide a data-quality limitation just because the dashboard looks better without it.**

Where source limitations were identified, they are explicitly documented so that stakeholders can distinguish between:

- Observed platform behavior
- Analytical interpretation
- Data-quality limitations
- Recommendations requiring additional validation

This helps ensure the dashboard remains useful as a decision-support tool without overstating what the data can prove.

---

## Final Takeaway

> **The Streaming Platform Analytics Dashboard transforms raw viewing activity into an interactive decision-support experience that connects user engagement, content performance, package behavior, geography, and regional drill-down.**

The dashboard is designed to move a stakeholder from:

**“How is the platform performing?”**

to:

**“What is happening in this province, which content matters, and what should the business investigate next?”**

---

## Author

**Brian Naufal**  
Data Analyst / Business Intelligence

**Tools:** Power BI • DAX • Power Query

- Portfolio: https://briannaufal-portfolio.netlify.app/
- LinkedIn: https://www.linkedin.com/in/brian-naufal-1b87771ba
- Email: brian.naufal5420@gmail.com
