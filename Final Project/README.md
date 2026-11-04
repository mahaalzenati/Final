
# 📦 StockPilot – Smart Inventory Management System

## 1. Project Overview

StockPilot is an AI-powered inventory management system designed to help small and medium-sized stores monitor inventory, analyze sales trends, and make informed replenishment decisions.

The system continuously monitors stock levels, detects products that are expected to run out within five days, and triggers an automated analysis process.

Using four specialized LLM-based roles, StockPilot evaluates sales forecasts, financial factors, and potential risks to recommend suitable replenishment scenarios. The final recommendation is sent to the store manager through Telegram for review and approval.

## 2. Problem & Target Users

### The Problem

Traditional inventory management often depends on manual monitoring and periodic stock checks. This can lead to:

- Late detection of low-stock products.
- Lost sales opportunities due to stockouts.
- Overstocking caused by inaccurate replenishment decisions.
- Difficulty analyzing sales trends and future demand.
- Replenishment decisions made without considering financial factors and potential risks.

### Target Users

- Small and medium-sized store owners.
- Store managers.
- Inventory managers and staff responsible for stock replenishment.

## 3. Proposed Solution & Key Features

StockPilot combines automated inventory monitoring, AI-based analysis, programmatic calculations, and human approval in one integrated solution.

### Key Features

- **Automated Inventory Monitoring:** Checks inventory data every 15 minutes and detects products expected to run out within five days.
- **Low-Stock Alerts:** Automatically generates alerts when inventory reaches the defined threshold.
- **Multi-Agent AI Analysis:** Uses four specialized LLM-based roles to analyze different aspects of replenishment decisions.
- **Sales Analysis:** Evaluates sales patterns and provides demand forecasts and assumptions.
- **Financial Analysis:** Examines financial and cost-related factors affecting replenishment decisions.
- **Risk Assessment:** Identifies potential risks and uncertainties.
- **Replenishment Scenario Calculation:** Calculates alternative replenishment quantities and costs programmatically.
- **Smart Recommendation:** The Manager Agent evaluates the available scenarios and selects the most suitable option based on the analyses and calculated results.
- **Human Approval:** Sends recommendations to the manager through Telegram, allowing approval or rejection before execution.
- **Centralized Dashboard:** Provides visibility into inventory, alerts, recommendations, decisions, and replenishment orders.
- **Inventory Simulation:** Allows users to simulate sales and order receiving to test inventory updates.

## 4. Technology Stack

| Technology | Role |
|---|---|
| n8n | Workflow automation and orchestration |
| Supabase | Central database and data management |
| Lovable | Dashboard development |
| Telegram Bot | Notifications and manager approval |
| LLMs | Specialized analysis and recommendation generation |
| n8n Code Nodes | Scenario calculations and output validation |

### AI Architecture

StockPilot follows a multi-agent AI architecture consisting of four specialized LLM-based roles:

1. **Sales Agent:** Analyzes sales data and provides demand forecasts and assumptions.
2. **Finance Agent:** Evaluates financial and cost-related factors.
3. **Risk Agent:** Identifies potential risks and uncertainties.
4. **Manager Agent:** Evaluates the calculated scenarios and selects the most suitable recommendation.

All four roles are implemented using n8n Basic LLM Chain nodes.

Numerical calculations are handled separately by n8n Code Nodes rather than being left to the LLMs.

## 5. How It Works

StockPilot operates through four main automated workflows.

### Workflow 1: Inventory Monitoring

- Runs automatically every 15 minutes.
- Retrieves inventory data from Supabase.
- Checks the expected stock coverage for each product.
- Generates a low-stock alert when a product is expected to run out within five days.

### Workflow 2: AI Analysis & Recommendation

- Receives the low-stock alert.
- Sends relevant data to the Sales, Finance, and Risk Agents.
- Collects their analyses and assumptions.
- Calculates alternative replenishment scenarios using n8n Code Nodes.
- Sends the analyses and calculated scenarios to the Manager Agent.
- The Manager Agent selects a suitable scenario and explains its decision.
- Validates the generated recommendation.
- Sends the recommendation to the manager through Telegram.

### Workflow 3: Manager Response & Order Processing

- Receives the manager's response through Telegram.
- If approved, creates a replenishment order in Supabase and updates the decision status.
- If rejected, updates the decision status to Rejected without creating an order.

### Workflow 4: Inventory Simulation

- Triggered manually through the dashboard.
- Simulates sales transactions and order receiving.
- Updates inventory records in Supabase.
- Designed for testing and demonstration purposes.

### System Architecture

The system uses Supabase as its centralized database, while n8n orchestrates the automated workflows and Lovable provides the dashboard interface.

Telegram serves as the notification and approval channel.

## 6. Setup or Access Instructions

StockPilot is an integrated application that depends on configured external services rather than a standalone application.

To access or reproduce the system, the following components must be configured:

1. **Supabase:** Set up the database tables and required project credentials.
2. **n8n:** Configure the four workflows, database connections, and required LLM credentials.
3. **Telegram Bot:** Configure the bot and connect it to the notification and approval workflows.
4. **Lovable Dashboard:** Connect the dashboard to Supabase to display and manage system data.

> Note: The required credentials and API keys should be configured securely and must not be committed to the repository.

## 7. Demo

- **Live Dashboard:** [Add Dashboard Link]
- **Demo Video:** [Add Demo Video Link]

## 8. Known Limitations

- AI-generated forecasts and assumptions depend on the quality and availability of the input data.
- The system's replenishment recommendations are decision-support suggestions and require human approval before an order is created.
- Numerical calculations are based on the implemented business rules and available input data.
- The inventory simulation is intended for testing and demonstration, not as a replacement for real sales and receiving operations.
- The system currently depends on configured external services, including Supabase, n8n, Telegram, and an LLM provider.

## 9. Project Structure

[Add the final repository folder structure here.]

## 10. Future Improvements

- Improve demand forecasting using historical sales data.
- Add more advanced inventory analytics.
- Support additional business rules and replenishment constraints.
- Expand reporting and performance indicators.
- Improve scenario evaluation as more operational data becomes available.

---

**StockPilot – Stay Ahead of Demand, Not Behind It.**
