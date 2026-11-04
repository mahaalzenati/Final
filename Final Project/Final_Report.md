# 📘 StockPilot – Final Project Report

## 1. Project Summary

StockPilot is an AI-powered inventory management system developed to improve how small and medium-sized stores monitor inventory and make replenishment decisions.

The project addresses common inventory management challenges, including delayed detection of low-stock products, missed sales opportunities, and replenishment decisions made without sufficient analysis.

The proposed solution integrates automated monitoring, specialized AI-based analysis, programmatic scenario calculations, and human approval.

Supabase acts as the centralized database, n8n orchestrates the workflows, Lovable provides the dashboard, and Telegram enables notifications and manager approval.

## 2. Problem & Proposed Solution

### 2.1 Problem

Manual inventory monitoring can make it difficult for store managers to identify products approaching stockout at the right time.

This may result in:
- Lost sales opportunities.
- Delayed replenishment decisions.
- Excess inventory.
- Poor consideration of financial factors and potential risks.

### 2.2 Proposed Solution

StockPilot continuously monitors inventory and automatically triggers an analysis process when a product's expected stock coverage falls below five days.

The system then analyzes the situation from sales, financial, and risk perspectives, calculates alternative replenishment scenarios, and generates a recommendation for the manager.

The final decision remains under human control.

## 3. System Design & Architecture

### 3.1 Architecture Overview

StockPilot is built around a centralized database and automated workflows orchestrated by n8n.

The architecture consists of:

- **Supabase:** Stores inventory data, alerts, analysis results, decisions, and replenishment orders.
- **n8n:** Coordinates monitoring, analysis, calculations, validation, and approval workflows.
- **LLM-based Roles:** Perform specialized analysis and support replenishment decisions.
- **Lovable:** Provides the dashboard interface.
- **Telegram Bot:** Delivers alerts and recommendations and receives manager responses.

### 3.2 Tool Selection Decisions

| Tool | Reason for Selection |
|---|---|
| Supabase | Provides a centralized database for managing and synchronizing system data. |
| n8n | Enables visual workflow orchestration and integration between services. |
| Lovable | Supports the development of an interactive dashboard. |
| Telegram Bot | Provides a direct communication channel for notifications and manager decisions. |
| LLMs | Enable contextual analysis of sales, financial, and risk-related information. |

### 3.3 Workflow Design

The system is divided into four workflows:

#### Workflow 1 – Inventory Monitoring

Runs every 15 minutes, retrieves inventory data from Supabase, evaluates stock coverage, and generates alerts for products expected to run out within five days.

#### Workflow 2 – AI Analysis & Recommendation

Receives low-stock alerts and coordinates four specialized LLM-based roles.

The Sales, Finance, and Risk roles analyze the available data and provide their respective insights and assumptions.

n8n Code Nodes calculate alternative replenishment scenarios, including quantities and costs.

The Manager Agent then evaluates the analyses and calculated scenarios, selects a suitable option, and provides a justification.

A Code Node validates the output before the recommendation is sent through Telegram.

#### Workflow 3 – Manager Response & Order Processing

Receives the manager's decision through Telegram.

- **Approved:** Creates a replenishment order in Supabase and updates the decision status.
- **Rejected:** Updates the decision status to Rejected without creating a replenishment order.

#### Workflow 4 – Inventory Simulation

A separate workflow triggered through the dashboard.

It simulates sales transactions and order receiving, then updates inventory data in Supabase.

This workflow supports project testing and demonstration and is not part of the core replenishment decision process.

## 4. AI Integration & Added Value

### 4.1 Multi-Agent AI Architecture

StockPilot uses four specialized LLM-based roles, each responsible for a different aspect of the replenishment decision.

| Role | Responsibility |
|---|---|
| Sales Agent | Analyzes sales data and provides demand forecasts and assumptions. |
| Finance Agent | Analyzes financial and cost-related factors. |
| Risk Agent | Identifies potential risks and uncertainties. |
| Manager Agent | Evaluates the available scenarios and selects the most suitable recommendation. |

Each role has a distinct responsibility, prompt, and input context.

The four roles are implemented using n8n Basic LLM Chain nodes.

### 4.2 Why Separate AI Roles?

Separating the analysis into specialized roles helps organize the decision-making process.

Instead of relying on one general prompt to analyze every aspect, each role focuses on a specific perspective.

This makes the analysis more structured and allows the Manager Agent to consider multiple factors before selecting a scenario.

### 4.3 AI vs. Programmatic Calculations

An important design decision was to separate AI-based analysis from numerical calculations.

- LLM-based roles provide analysis, forecasts, assumptions, and recommendations.
- n8n Code Nodes calculate replenishment quantities and scenario costs.
- Code validation checks the Manager Agent's generated output before it is sent.

This separation reduces reliance on LLMs for numerical operations and makes calculations more consistent with the implemented business rules.

### 4.4 Human-in-the-Loop Decision Making

AI-generated recommendations are not executed automatically.

The manager receives the recommendation through Telegram and decides whether to approve or reject it.

This ensures that the final replenishment action remains under human control.

## 5. Testing & Validation

Practical tests were conducted to verify the main system functions.

### Test Case 1: Discounted Product – Increased Demand

**What Was Tested?**

A product with an active discount and stock expected to last fewer than five days was tested to verify the system's ability to detect low inventory and analyze the potential impact of the promotion on future demand.

**Expected Result**

- Detect the low-stock condition and generate an alert.
- Analyze the potential impact of the discount on demand.
- Evaluate financial factors and potential risks.
- Calculate alternative replenishment scenarios.
- Select a suitable scenario through the Manager Agent.
- Send the recommendation to the manager through Telegram.

**Actual Result**

**Status: Passed**

The system worked as expected. It successfully detected the low-stock condition, executed the analysis workflow, and generated a replenishment recommendation based on the specialized agents' analyses and the calculated scenarios.

### Test Case 2: Non-Discounted Product – Variable Demand

**What Was Tested?**

[Document the test after execution.]

**Expected Result**

The system should analyze the product's sales behavior without an active promotion, evaluate financial factors and potential risks, and generate a suitable replenishment recommendation.

**Actual Result**

[Add the actual result.]

**Status:** [Passed / Failed / Needs Improvement]

### Additional Validation

Further tests can be documented to verify:

- Manager approval and replenishment order creation.
- Manager rejection without order creation.
- Inventory updates after simulation.
- Dashboard synchronization with Supabase.

## 6. Improvements & Prompt Refinement

Prompt refinement was an important part of improving the system's outputs and user interface.

### 6.1 Dashboard Prompt Improvement

The dashboard prompt was refined to improve the presentation and organization of the existing interface.

**Impact:**

- Improved the dashboard's overall visual appearance and user experience.
- Established a more consistent visual identity aligned with StockPilot's brand colors.
- Improved layout organization, spacing, and visual hierarchy.
- Enhanced Arabic text alignment and readability, especially in alert and notification details.
- Made inventory information, alerts, and recommendations easier to read and understand.
- Created a cleaner and more professional interface while preserving the existing functionality and content.

### 6.2 AI Agent Prompt Documentation

The prompts for the four specialized roles were documented separately to clarify their responsibilities and expected outputs.

The documented prompts include:

- Sales Agent Prompt.
- Finance Agent Prompt.
- Risk Agent Prompt.
- Manager Agent Prompt.

Each prompt is maintained in a separate Markdown file.

### 6.3 Social Media Prompt

A dedicated prompt was prepared to generate StockPilot social media content while maintaining the project's visual identity and communication style.

The prompt documentation is available in the project's marketing materials.

## 7. Responsible AI Considerations

Several considerations were taken into account when integrating AI into StockPilot:

### 7.1 Human Oversight

AI recommendations do not directly create replenishment orders. A human manager must approve the recommendation before execution.

### 7.2 Separation of Responsibilities

Each AI role has a defined responsibility to avoid mixing different analysis tasks.

### 7.3 Numerical Reliability

Replenishment quantities and costs are calculated programmatically rather than generated directly by LLMs.

### 7.4 Output Validation

The Manager Agent's output passes through a Code Node validation step before being sent to the manager.

### 7.5 Transparency

The system provides a recommendation with a justification, helping the manager understand the factors considered in the decision.

### 7.6 Data Quality

The quality of AI analysis depends on the accuracy and completeness of the available inventory and sales data. Generated forecasts and assumptions should therefore be reviewed as decision-support information rather than guaranteed predictions.

## 8. Current Limitations

- Forecast quality depends on the available sales history and input data.
- AI-generated analyses may contain assumptions that require human review.
- The system currently uses a fixed low-stock threshold of five days.
- Scenario calculations depend on the implemented business rules and available data.
- The inventory simulation is intended for demonstration and testing.
- The system depends on external services and their availability.

## 9. Future Improvements

Potential future improvements include:

- Developing more advanced demand forecasting methods.
- Supporting dynamic low-stock thresholds based on product behavior.
- Adding more financial and operational constraints to scenario calculations.
- Improving risk analysis using additional business data.
- Expanding dashboard analytics and reporting.
- Adding historical performance tracking to evaluate recommendation quality.
- Supporting additional notification and approval channels.

## 10. Conclusion

StockPilot demonstrates how workflow automation and specialized LLM-based analysis can be combined to support inventory replenishment decisions.

By integrating automated monitoring, multi-perspective analysis, programmatic calculations, and human approval, the system provides a structured approach to identifying low-stock situations and evaluating replenishment options.

The project highlights the value of combining AI capabilities with deterministic business logic and human oversight rather than relying on AI-generated decisions alone.
