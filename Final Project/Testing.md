## Test Case 1: Discounted Product – Increased Demand

### 1. What Was Tested?
A product with an active discount and stock expected to last fewer than 5 days was tested to verify StockPilot's ability to detect low inventory, analyze the impact of the promotion on future demand, and generate a suitable replenishment recommendation.

### 2. Expected Result
- Detect the low-stock condition and automatically generate an alert.
- Sales Agent analyzes the potential impact of the discount on future demand.
- Finance Agent evaluates costs and financial factors.
- Risk Agent identifies potential risks.
- Calculate alternative replenishment scenarios.
- Manager Agent evaluates the scenarios and selects the most suitable option.
- Send the final recommendation to the manager through the Telegram Bot.

### 3. Actual Result
<badge color="success">Passed</badge>

The system worked as expected. It successfully detected the low-stock condition, executed the analysis workflow, and generated a replenishment recommendation based on the specialized agents' analyses and the calculated scenarios.

[Result](./Screenshoys/T1.png)
