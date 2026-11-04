# 📊 StockPilot Dashboard – Prompt Documentation

## 1. Project Overview

Documentation of the prompts used to build and refine the StockPilot dashboard using Lovable.

## 2. Dashboard Objective

Create a centralized dashboard for monitoring inventory operations, low-stock alerts, replenishment recommendations, manager decisions, and replenishment orders.

## 3. Development Tool

- **Platform:** Lovable
- **Database:** Supabase

## 4. Main Prompt

Lovable Prompts: AI Business Operations Copilot

Use these in TWO stages. Paste Prompt 1 first, check it works, then paste Prompt 2.

Before pasting: connect your Supabase project to Lovable (Supabase integration) and use the anon key only.

---

## PROMPT 1: Manager Dashboard (read-only)

```
Build a clean, modern web dashboard called "AI Business Operations Copilot".
It is a manager's control panel for a system that monitors company inventory, uses a team of AI agents to analyze problems, and recommends decisions that the manager approves.

IMPORTANT RULES
- The database already exists in my connected Supabase project. Do NOT create, alter or migrate any tables. Do NOT insert sample data. Read real data from Supabase only.
- Use the Supabase anon key only. This dashboard is READ-ONLY in this step. Never use or mention a service_role key.
- UI language: English, left-to-right. Some text fields come from the AI agents in Arabic: render every free-text value with dir="auto" so Arabic displays correctly.
- Show loading skeletons and friendly empty states ("No open alerts. Everything looks healthy.").

DATABASE (already exists)
- products: id, name, sku, stock_quantity, unit_cost, unit_price, supplier_id, status ('normal' | 'ordered')
- suppliers: id, name, email, lead_time_days
- sales: id, product_id, quantity, sold_at
- detection_rules: id, name, metric, operator, threshold, severity, is_active
- alerts: id, rule_id, product_id, metric_value, status ('open' | 'analyzed' | 'closed'), created_at
- agent_analyses: id, alert_id, agent_name ('sales_ops' | 'finance' | 'risk' | 'manager'), analysis (jsonb), created_at
- decisions: id, alert_id, recommended_action, recommended_quantity, reasoning, risk_level, status ('pending' | 'approved' | 'rejected'), decided_at, created_at
- purchase_orders: id, decision_id, product_id, supplier_id, quantity, status ('ordered' | 'received'), expected_arrival, created_at, received_at
- business_events: id, product_id (nullable = all products), event_type, title, start_date, end_date
- View v_stock_days_left: product_id, name, stock_quantity, status, avg_daily_sales, days_left

PAGE LAYOUT (single page, top to bottom)

1) Header
- Title "AI Business Operations Copilot" and subtitle "Multi-agent monitoring with manager approval".
- A small "Live" indicator (green dot) showing the data auto-refreshes.

2) Four KPI cards
- Open alerts: count of alerts with status 'open' or 'analyzed'.
- Decisions awaiting approval: count of decisions with status 'pending'.
- Orders in transit: count of purchase_orders with status 'ordered'.
- Products at risk: count of rows in v_stock_days_left where days_left < 5.

3) Alerts table
- Columns: Product (name), Issue (rule name, or "Low stock" if rule_id is null), Value (metric_value as "X days left"), Severity (from the rule, default "High"), Time (relative, e.g. "5 minutes ago"), Status (badge: open = red, analyzed = amber, closed = gray).
- Newest first. Clicking a row selects it and loads section 4 for that alert. The newest non-closed alert is selected by default. Highlight the selected row.

4) Alert details: agent analysis and decision (the most important section)
For the selected alert, show four cards, using agent_analyses (match alert_id and agent_name; the analysis column is a flat JSON object) and the decisions row for that alert:

- Sales/Ops Agent card ("What happened to demand?"): demand_assessment, likely_cause (badge), duration_outlook (badge), suggested_quantity, quantity_reasoning, confidence (badge), evidence (bullet list), data_gaps (bullet list).
- Finance Agent card ("What do the options cost?"): order_cost_assessment, stockout_impact, overstock_risk (badge), overstock_reasoning, chosen_scenario, recommended_quantity, financial_reasoning, confidence, evidence (list), data_gaps (list).
- Risk Agent card ("What could go wrong?"): overall_risk_level (badge), risks (list; each item shows category, level badge, description, evidence), risk_of_not_ordering, risk_of_ordering_too_much, mitigations (list), requires_human_attention (warning badge with human_attention_reason), confidence, data_gaps.
- Manager recommendation card (full width, visually the most prominent, with an accent border): 
  - summary as a large headline text.
  - Action and quantity from the decision row (recommended_action, recommended_quantity).
  - Order cost from the manager analysis: analysis.validation.order_cost, formatted as currency.
  - reasoning, agent_agreement (badge: agree = green, partial = amber, disagree = red), disagreements (list), risk_level badge, confidence.
  - conditions_before_approval as a checklist titled "Check before approving".
  - A warning badge "Human review required" when requires_human_attention is true.
  - If analysis.validation.corrected is true, show an amber badge "Corrected by validation rules" with the notes from analysis.validation.notes.
  - Decision status badge: pending = "Awaiting your approval" (amber), approved = green, rejected = red, plus decided_at if present.
Render everything as readable UI (badges, lists, labeled fields). Never show raw JSON. If a field is missing, skip it gracefully. If the analysis for an agent does not exist yet, show "Analysis in progress".

5) Inventory status (two-column area, left side)
- Table from v_stock_days_left: Product, Stock, Avg daily sales, Days left, Status.
- Status badge: days_left < 5 = red "At risk", 5 to 10 = amber "Watch", above 10 = green "Healthy", null = gray "No recent sales". If the row's status is 'ordered', show a blue "Ordered" badge instead.
- Sort by days_left ascending (nulls last).

6) Purchase orders (two-column area, right side)
- Table from purchase_orders joined with products and suppliers: Order id (short), Product, Quantity, Supplier, Expected arrival, Status badge (ordered = blue, received = green).
- Newest first. Empty state: "No purchase orders yet."

7) Activity timeline
- A vertical timeline of the latest 20 events, newest first, built from timestamps in these tables: alert created ("Alert: low stock detected for <product>"), decision created ("Agents recommended ordering <qty> units"), decision decided ("Manager approved / rejected"), purchase order created, purchase order received.

8) Business events (small card at the bottom)
- List of business_events whose end_date is today or later: title, type badge, date range, and product name or "All products". Read-only. Caption: "Context the agents use to explain demand changes."

DATA REFRESH
- Subscribe to Supabase Realtime on: alerts, decisions, purchase_orders, products, agent_analyses. On any change, refetch the affected data.
- Also refetch everything every 10 seconds as a fallback (the stock view depends on the sales table, which is not subscribed).
- Update the page without a full reload and without losing the selected alert.

DESIGN
- Clean, professional admin look, lots of whitespace, rounded cards, soft shadows, a restrained palette (neutral grays plus red, amber, green and blue only for status).
- Responsive: stacks to one column on mobile; tables scroll horizontally if needed.
- Use consistent badge components for all statuses.
```

---

## PROMPT 2: Demo controls and action buttons (after Prompt 1 works)

```
Extend the dashboard with a demo simulator and action buttons that call n8n webhooks. The dashboard stays read-only toward Supabase: ALL writes happen through these webhook calls, never directly to the database.

CONFIG
- Create a single config file (src/config.ts) with:
  - N8N_BASE_URL (placeholder "https://YOUR-N8N-URL/webhook")
  - WEBHOOK_SECRET (placeholder "CHANGE_ME"), sent as the header "x-api-key" on every request.
  - ENABLE_DECISION_BUTTONS = false
- Every webhook call: POST with JSON body, expect JSON like { "ok": true } or { "ok": false, "error": "..." }. Show a success or error toast with the message. Disable the button while the request is running. Handle network errors and CORS failures with a clear error toast.

A) Demo simulator card (placed at the very bottom of the page, collapsible, collapsed by default)
- Title: "Company Simulator (demo only)". Subtitle: "Simulates the company's sales system and warehouse. In a real deployment this is replaced by an API integration. It is not part of the manager's tool."
- Visually separated from the rest: dashed border and a muted background.
- "Simulate sale" form: product dropdown (from products, showing name and current stock), quantity number input, and a "Sell" button. Validation: quantity must be an integer greater than 0 and not greater than the product's current stock; show an inline error otherwise. On submit: POST {N8N_BASE_URL}/simulate-sale with { "product_id": "...", "quantity": 12 }.
- "Simulate shipment arrival" form: dropdown of purchase_orders with status 'ordered' (showing product name, quantity, expected arrival) and a "Mark as received" button. If there are none, show "No orders in transit." On submit: POST {N8N_BASE_URL}/receive-shipment with { "purchase_order_id": "..." }.

B) "Mark as received" shortcut in the Purchase orders table
- For rows with status 'ordered', show a small "Mark as received" button that calls the same receive-shipment webhook. Confirm with a small dialog first. Rows already received show no button.

C) Approve / Reject buttons on the Manager recommendation card
- Only render when ENABLE_DECISION_BUTTONS is true AND the decision status is 'pending'.
- "Approve" and "Reject" buttons (with a confirmation dialog showing the product, quantity and order cost). On confirm: POST {N8N_BASE_URL}/decision with { "decision_id": "...", "action": "approve" } or "reject".
- When the decision status is not 'pending', show no buttons.

After any successful webhook call, refetch data immediately (do not wait for the realtime event).
```

---

## 5. Refinement Prompts

### 5.1 UI and Visual Identity

Make INCREMENTAL changes to the existing dashboard. Do NOT rebuild the project, do NOT recreate files from scratch, do NOT remove or rewrite existing sections, queries, realtime subscriptions or logic. Edit only what is needed for the items below, and keep everything else exactly as it is. Do NOT create, alter or migrate any tables and do NOT insert sample data. All writes go ONLY through the n8n webhooks, using the existing src/config.ts (N8N_BASE_URL and the "x-api-key" header).

THEME TOGGLE (light / dark)
Add a Sun/Moon toggle button in the header (lucide-react). Save the choice in localStorage, default to the system preference.
Apply it with CSS variables / Tailwind tokens so existing components (cards, tables, badges, dialogs) support both themes. Add a 200ms transition.
Palette (electronics / tech feel):
Light: background #F4F7FB, card #FFFFFF, border #E2E8F0, text #0F172A, muted #64748B, primary #4F46E5, accent #06B6D4.
Dark: background #0B1220, card #111A2E, border #1E2A44, text #E5EDF9, muted #94A3B8, primary #818CF8, accent #22D3EE.
Status colors (same in both themes): danger #EF4444, warning #F59E0B, success #10B981, info #3B82F6. Badges use a soft tinted background (about 12% opacity) with the full color as text.
HEADER IMAGE
Turn the existing header into a banner with an electronics background image (circuit board / microchip, e.g. from Unsplash) and a dark indigo gradient overlay. If the image fails to load, fall back to an SVG circuit-line pattern.
Add a Cpu icon next to the title.
ICONS
Add lucide-react icons to the existing KPI cards: AlertTriangle (open alerts), Clock (awaiting approval), Truck (orders in transit), PackageX (products at risk), each in a colored circular background.
Add a small icon next to each product name, guessed from the name (Laptop, Smartphone, Headphones, Monitor, Keyboard, Mouse, Camera, Watch, Tablet, Printer; fallback: Package).
CHARTS (recharts, themed with the CSS variables, with tooltips and responsive containers) Add a responsive grid right under the KPI cards (2 columns on desktop, 1 on mobile) with:
"Sales trend": area chart of total units sold per day for the last 14 days (from the sales table), with a product filter dropdown (All products by default).
"Days of stock left by product": horizontal bar chart from v_stock_days_left, red under 5, amber 5 to 10, green above 10, with a dashed reference line at 5 days.
"Alerts by status": donut chart (open red, analyzed amber, closed gray) with the total in the center. Add friendly empty states and skeleton loaders. These charts should refresh with the existing realtime/10-second refetch.
SIMULATOR: REPLACE THE OLD ONE
Remove only the old "Company Simulator" card at the bottom, and replace it with a right-side drawer (Sheet) opened by a "Simulator" button in the header. Title: "Company Simulator (demo only)".
Inside the drawer, ONE simple form: a) Product dropdown (from products) showing the product icon, name and "Stock: N". b) Quantity input (integer, min 1) with - / + stepper buttons. c) Two buttons side by side:
"Sell" (ShoppingCart icon): validate quantity is an integer > 0 and not greater than the product's current stock, otherwise show an inline error. On click: POST {N8N_BASE_URL}/simulate-sale with { "product_id": "...", "quantity": N }.
"Receive shipment" (PackageCheck icon, green): find the oldest purchase_order with status 'ordered' for the selected product. If found, show a helper line "Order of X units, expected <date>" (the quantity field is ignored, the order's own quantity is used) and on click POST {N8N_BASE_URL}/receive-shipment with { "purchase_order_id": "..." }. If none exists, disable the button and show "No order in transit for this product."
Below the form, show the last 5 sales from the sales table (product, quantity, relative time).
Every call: disable buttons while running, spinner on the clicked button, success/error toast with the message, clear handling of network/CORS errors, and refetch all data immediately after success.
Keep the "Mark as received" shortcut in the Purchase orders table unchanged.
POLISH
Sticky table headers and subtle row hover. Keep dir="auto" on free-text values. Keep all existing sections (alerts table, agent analysis, inventory, purchase orders, timeline, business events) working exactly as before, only restyled to the new theme.

### 5.2 Dashboard Components

The previous update improved the visual styling,

but the alert details are still permanently visible

on the main dashboard.

I need you to fix the display behavior.

REQUIREMENTS:

Keep the main dashboard showing only the

alerts list, without displaying their detailed

content by default.

When the user clicks an alert, expand that

specific alert and display its existing details

directly below it.

The expanded content must include all existing

information:

Alert details

AI recommendations

AI agents analysis

When the user clicks the same alert again,

collapse its details and hide the expanded content.

Only display details for the selected alert.

Do not show all alert details simultaneously.

Preserve all existing data, AI-generated

content, functionality, and relationships.

Do not create new pages, modals, or separate

dashboard sections.

Keep the previously requested StockPilot

branding, colors, dark theme, spacing, and

Arabic RTL / English LTR formatting.

IMPORTANT:

This is a functional UI behavior change,

not another styling-only update.

The default state must show collapsed alerts.

Details should appear ONLY after clicking

an individual alert.
