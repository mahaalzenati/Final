
# AI Client Intake & Request Routing System
[English](README.md) | [العربية](README.ar.md)

Automating client request intake using Zapier, summarizing requests with AI, validating information completeness, and automatically routing each request to the appropriate path based on its status.

---

## 🎯 Problem

### The Context

A service company receives requests from potential clients and needs to analyze each request to understand client needs, organize information, and determine the appropriate next step.

### The Problem

The company relies on manual processing of client requests. Employees review each request to understand its content, extract key information, verify its completeness, and determine the appropriate action.

As the number of requests increases, this process becomes more time-consuming and effort-intensive. It may also lead to delayed responses to clients or make it difficult to identify missing information.

### Why It Matters

Improving this process helps reduce the time and effort required to handle requests, accelerate client responses, and improve information organization and accuracy.

It also allows employees to focus on evaluating client needs and making appropriate decisions instead of spending excessive time on manual review and classification.

---

## 💡 Solution

A structured workflow was designed to receive and process client requests, starting with collecting the request and understanding client needs, followed by extracting, organizing, and validating information completeness, and finally determining the appropriate action and routing the request to the responsible person.

The process also includes recording processing results and notifying the responsible person. This helps improve request organization, reduce manual effort, and make it easier to track each request and determine the appropriate next step.

### What does the system do?

1. **Request Intake:** Collect client requests through Google Forms and record them in Google Sheets.
2. **Request Understanding:** Analyze request content to identify client needs and the required service.
3. **Information Extraction:** Summarize the request and extract key details, such as budget and timeline when available.
4. **Data Validation:** Identify missing information and verify that the request is clear and can be processed.
5. **Routing Decision:** Route requests that meet the requirements for follow-up, while sending requests that need clarification or verification for human review.
6. **Result Logging:** Update the request record with processing results, status, and assigned route.
7. **Notifications:** Notify the relevant person about requests ready for follow-up or those requiring review.

---

## 👤 Users

**Primary Users:**

- Employees responsible for evaluating requests, determining the next step, and following up on their execution.

**User Need:**

- Simplify and accelerate the processing of new business requests.
- Clearly understand client needs and project requirements.
- Organize project information and verify its completeness.
- Make it easier to evaluate requests and determine the appropriate next step for each project.
- Reduce manual effort and improve the efficiency of client request follow-up.

---

## 🧠 How I Designed the Solution

The solution was designed to automate the initial stages of processing business requests while maintaining human involvement in reviewing requests that require intervention.

The system uses AI to understand requests and extract important information, alongside predefined rules to validate data completeness and determine the appropriate route for each request.

Google Forms was selected for collecting requests, while Google Sheets is used to store them and track their status. Notifications are also sent to simplify follow-up and accelerate appropriate actions.

---

## ⚙️ How It Works

```text
┌──────────────────────────────────────┐
│                Input                 │
│       Submit a business request      │
│           via Google Forms           │
└──────────────────┬───────────────────┘
                   ↓
┌──────────────────────────────────────┐
│            Data Storage              │
│      Record the request in           │
│          Google Sheets               │
└──────────────────┬───────────────────┘
                   ↓
┌──────────────────────────────────────┐
│           AI Processing              │
│    Understand and summarize the      │
│       request and extract key        │
│            information               │
└──────────────────┬───────────────────┘
                   ↓
┌──────────────────────────────────────┐
│        Validation & Routing          │
│      Validate information            │
│       completeness and determine     │
│         the appropriate route        │
└──────────────────┬───────────────────┘
                   ↓
┌──────────────────────────────────────┐
│               Output                 │
│       Update the request record      │
│       and notify the relevant        │
│               person                 │
└──────────────────┬───────────────────┘
                   ↓
           ┌───────┴────────┐
           ↓                ↓
┌─────────────────┐  ┌─────────────────┐
│ Ready for       │  │ Human Review    │
│ Follow-up       │  │                 │
└─────────────────┘  └─────────────────┘
```

---

## 🤖 Role of AI

### What does AI do in this solution?

AI is used to process business requests by understanding their content and extracting important information. Its responsibilities include:

- **Request Understanding:** Analyze the business request text and identify the service the client needs.
- **Request Summarization:** Generate a clear summary of project requirements.
- **Information Extraction:** Identify key details, such as service type, budget, and timeline when available.
- **Missing Information Detection:** Identify unavailable information that may be necessary to understand and evaluate the request.
- **Decision Support:** Provide the information needed to apply validation rules and determine whether a request is ready for follow-up or requires human review.

### What AI Should NOT Do

- **Assume Missing Information:** Never guess the budget, timeline, or any details that the client has not provided.
- **Override Defined Business Rules:** Requests must be processed according to the rules and criteria established in the system.
- **Bypass Human Review:** Unclear requests or those requiring additional verification must be forwarded to the responsible employee.
- **Make Promises or Commitments to Clients:** Never confirm prices, delivery dates, or project approval without human authorization.
- **Modify Request Data Without Justification:** Preserve the client's original information while recording analysis results separately and clearly.

---

## 🔄 Automation

### What parts of the process are automated?

- **Request Intake and Registration:** Collect business requests through Google Forms and automatically store them in Google Sheets.
- **Request Analysis:** Use AI to understand request content, identify the required service, and summarize project requirements.
- **Information Extraction:** Extract key details, such as budget and timeline, when available.
- **Initial Validation:** Check information completeness and request clarity, and identify missing details.
- **Request Routing:** Apply predefined rules to route requests that are ready for follow-up or those requiring human review.
- **Record Updates:** Log processing results and update the request status and assigned route.
- **Notifications:** Notify the relevant person about the processing result and required action.

---

## 🗂️ Data

### Input

- Client name.
- Email address.
- Client request.

### Output

- **Processed Request:** A processed business request with summarized requirements and extracted key information.
- **Validation Results:** The result of checking information completeness and identifying missing details.
- **Routing Decision:** Determines whether the request is ready for follow-up or requires human review.
- **Updated Record:** Updates the request record in Google Sheets with processing results and status.
- **Notification:** Sends a notification to the relevant person about the request and required action.

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| Google Forms | Collect business requests and client information |
| Google Sheets | Store requests, organize data, and update processing status |
| AI By Zapier | Understand requests, summarize them, extract key information, and detect missing details |
| Zapier | Connect and automate workflow stages |

---

## 🔑 Key Design Decisions

### Decision 1

**Decision:** `VALID`

Route the business request to the web team (`web_team`) when it meets all validation requirements, including complete client information, clear project details, and an available budget and timeline.

**Why:** To ensure that the request contains the necessary information for follow-up and reduce the need for additional communication with the client to complete missing details.

### Decision 2

**Decision:** `NEEDS_REVIEW`

Route the business request to human review (`human_review`) if it fails one or more validation requirements, such as missing budget or timeline information or unclear project requirements.

**Why:** To prevent incomplete or unclear requests from reaching the implementation team before they have been reviewed and the required information has been obtained.

---

## 🧪 Testing

### Test 1: Valid Client Request

**Input:**

\`\`\`text
Client: heba
Company: google
Request: We need a website for our company.
Budget: $5000
Timeline: next month
\`\`\`

**Expected Result:**

- `validation_status = VALID`
- `requires_human = false`
- `routing = web_team`
- Send a notification confirming receipt of a request that is ready for follow-up.

**Actual Result:**

The request was classified as valid and ready for follow-up. The system extracted the client's name, company, service type, budget, and timeline, and sent a notification confirming receipt of the request.

**Status:** ✅ Pass

---

### Test 2: Request Requiring Human Review

**Input:**

\`\`\`text
Client: lama
Company: google
Missing Information: budget
Original Request: We need a website for our company.
We need it next month.
\`\`\`

**Expected Result:**

- `validation_status = NEEDS_REVIEW`
- `requires_human = true`
- `routing = human_review`
- Send a notification confirming receipt of a request requiring human review.

**Actual Result:**

The request was classified as requiring human review.

**Status:** ✅ Pass

---

## 📸 Evidence

### Final Result

[Test1](./Screenshots/Test1.png)

[Test2](./Screenshots/Test2.png)

### Workflow

[Workflow](./Screenshots/workflow.png)

---

## 🔗 Project Links

**Workflow:** [https://zapier.com/editor/383094876/draft/383094876/fields]

**Repository:** [https://github.com/mahaalzenati/Final/tree/main]

---

## 👩‍💻 Author

**[Maha Alzenati]**

[LinkedIn](https://www.linkedin.com/in/maha-alzenati-gamedev/) · [GitHub](https://github.com/mahaalzenati)
