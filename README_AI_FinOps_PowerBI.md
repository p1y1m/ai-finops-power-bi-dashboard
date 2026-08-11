# AI FinOps Dashboard | Power BI

## Author: Pedro Yanez Melendez

## Overview

This project presents a Power BI dashboard designed to monitor the usage, cost, performance, and budget position of AI agents.

The report combines operational usage data with agent, model, budget, and calendar information to provide both an executive view and a detailed agent-level view. The dashboard is intended to support cost visibility, usage monitoring, and financial governance for AI-enabled solutions.

## Dashboard Pages

### 1. Executive Summary

The first page provides a compact management view of the main AI FinOps indicators.

It includes:

- Total AI cost
- Total tokens consumed
- Success rate
- Total budget
- Budget variance
- Monthly AI cost evolution
- AI cost by agent
- Month filter



The layout was designed to make the most important indicators visible immediately while keeping the page simple enough for executive review.

### 2. Agent Detail

The second page provides a more granular view of each AI agent.

It includes:

- Agent name
- Total cost
- Total tokens
- Success rate
- Budget
- Budget variance
- Month filter
- Business area filter

Conditional formatting was added to improve interpretation. Cost values use data bars, while budget variance uses background colors to highlight the financial position of each agent.



## Data Structure

The Power BI model uses five structured tables:

- **UsageTable** — AI usage, requests, tokens, cost, and operational metrics
- **AgentsTable** — agent information and business area
- **ModelsTable** — AI model information
- **BudgetsTable** — budget values by agent and month
- **CalendarTable** — calendar dimensions used for time-based analysis

The model connects usage and budget information with the corresponding agents and calendar dates, allowing the report to respond consistently to filters and time selections.

## Main Relationships

The report uses the following relationships:

- `UsageTable[Agent_ID]` → `AgentsTable[Agent_ID]`
- `BudgetsTable[Agent_ID]` → `AgentsTable[Agent_ID]`
- `UsageTable[Model_ID]` → `ModelsTable[Model_ID]`
- `UsageTable[Date]` → `CalendarTable[Date]`
- `BudgetsTable[Month_Start]` → `CalendarTable[Date]`

Relationships were configured with a many-to-one structure and single-direction filtering where appropriate.

## Core DAX Measures

The dashboard is driven by a small set of reusable measures.

```DAX
Costo total =
SUM(UsageTable[Total_Cost_USD])
```

```DAX
Solicitudes =
SUM(UsageTable[Requests])
```

```DAX
Tokens totales =
SUM(UsageTable[Total_Tokens])
```

```DAX
Tasa de éxito =
DIVIDE(
    SUM(UsageTable[Successful_Requests]),
    SUM(UsageTable[Requests]),
    0
)
```

```DAX
Presupuesto =
SUM(BudgetsTable[Budget_USD])
```

```DAX
Variación presupuesto =
[Presupuesto] - [Costo total]
```

A positive budget variance indicates remaining budget, while a negative value indicates that cost has exceeded the available budget.

## Build Process

The dashboard was built manually in Power BI Desktop following these main steps:

1. Import the structured Excel tables.
2. Review the model and create the required relationships.
3. Create the core DAX measures.
4. Format currency, percentage, and numeric measures.
5. Build the executive KPI cards.
6. Create the monthly cost trend chart.
7. Create the AI cost by agent chart.
8. Add the month slicer and refine the executive layout.
9. Apply a consistent visual style to the page.
10. Create a second page for detailed agent analysis.
11. Add the agent-level table and business filters.
12. Apply conditional formatting to cost and budget variance.
13. Review spacing, readability, titles, and final formatting.

A detailed visual build guide is also included in the repository to document the manual Power BI work step by step.

## Design Decisions

The report uses a restrained visual style focused on readability:

- Dark navy headers
- Light report background
- White visual containers
- Consistent Power BI blue for cost visualizations
- Soft green highlighting for favorable budget variance
- Dropdown slicers to reduce visual clutter
- Limited number of visuals per page

The objective was to keep the dashboard clear and practical rather than overload it with charts.

## Tools Used

- Microsoft Power BI Desktop
- Microsoft Excel
- DAX
- Power BI data modeling
- Conditional formatting
- Interactive slicers and filters

## Outcome

The final result is a two-page Power BI report that provides both high-level financial visibility and agent-level operational detail.

The project demonstrates practical Power BI work across data import, relationship modeling, DAX, KPI design, time-based analysis, filtering, conditional formatting, and dashboard presentation.
