
# XYZ Real Estate AI Agent — Intelligent Real Estate Lead Collection Agent

[English](README.md) | [العربية](README.ar.md)

An AI-powered agent built using n8n that helps XYZ Real Estate collect customer information and understand their real estate needs through Telegram conversations. It then validates the information and presents a final summary for confirmation before saving the data to Google Sheets.

## 📌 Project Overview

This project aims to automate the process of receiving requests from customers interested in buying or renting properties through an intelligent agent that manages conversations, understands the information provided by customers, identifies missing details, and asks only the necessary questions.

The agent does more than ask a sequence of questions. It relies on understanding customer messages, maintaining conversation context, applying business rules, and determining when external tools can be used.

The project focuses on ensuring that saved data is complete and valid according to predefined rules, and that the customer explicitly approves the final summary before the data is saved.

## 🎯 Problem Statement

Real estate companies need to collect structured customer information to understand their requirements and manage their requests efficiently.

The main challenges addressed by this project include:

- Manually collecting customer information, which may result in missing details.
- Repeating questions even when customers have already provided the answers in previous messages.
- Losing conversation context when receiving multiple messages from a customer.
- Ambiguous answers related to budget or expected timeline.
- Applying different business rules for property purchase and rental requests.
- Potentially saving incomplete or invalid data.
- Saving information before the customer confirms its accuracy.
- Informing customers that their data has been saved successfully without verifying the operation result.

## 💡 Proposed Solution

The project provides an AI-powered agent that receives customer messages through Telegram and manages the information collection and validation process until a final summary is confirmed.

The system enables the agent to:

- Welcome customers and initiate conversations.
- Understand the information provided by customers, even when multiple details are included in a single message.
- Retain previous answers and use them throughout the conversation.
- Identify missing fields and request only the missing information.
- Ask for clarification when an answer is ambiguous.
- Apply business rules based on the type of real estate request.
- Classify budgets into predefined categories.
- Validate data completeness and email addresses.
- Present a final summary containing all required fields.
- Wait for customer approval before saving the information.
- Save customer data to Google Sheets and verify the execution result.

## 👥 Target Audience

- Real estate companies.
- Real estate sales teams.
- Customer service representatives.
- Lead management teams.
- Companies looking to automate the intake of property purchase and rental requests.

## ⚙️ How the Project Works

1. **Message Reception:** The system receives the customer's message through the Telegram Trigger in n8n.
2. **Request Understanding:** The AI Agent analyzes the message and identifies the information provided by the customer.
3. **Context Retrieval:** The agent uses memory to access previous answers in the conversation.
4. **Missing Information Detection:** It compares the available information with the required fields and asks only the necessary questions.
5. **Data Validation:** It reviews the values and applies the business rules for purchase and rental requests.
6. **Summary Presentation:** It presents the nine data fields to the customer and asks them to confirm their accuracy.
7. **Information Updates:** If the customer corrects any information, the system updates it and presents a new summary for confirmation.
8. **Data Storage:** After receiving explicit confirmation, the agent uses the Google Sheets tool to add the data.
9. **Result Verification:** The system checks the saving operation result before informing the customer that the process was successful.

## 🧠 Role of Artificial Intelligence

The project uses AI to understand customer messages and manage the information collection process, rather than simply generating text responses.

The agent is responsible for:

- Understanding messages written in natural language.
- Extracting information related to the property, budget, and personal details.
- Using information previously provided by the customer.
- Identifying the appropriate next step based on missing fields.
- Requesting clarification when information is ambiguous.
- Applying conditional business rules.
- Preparing the final summary and updating it when information is corrected.
- Determining when the data-saving tool is allowed to be used.

### AI Usage Guidelines

- Never invent information that the customer has not provided.
- Never guess ambiguous values.
- Do not repeat questions about information that has already been clearly provided.
- Never save data before receiving explicit confirmation.
- Never claim that data has been saved successfully without verifying the tool's result.
- Maintain the independence of each customer's data from other customers' conversations.

## 🔄 Automation and Workflow

The project uses n8n to connect message reception, information processing, memory, the data-saving tool, and response delivery.

### Main Workflow Diagram

```text
Telegram Trigger
       |
       v
    AI Agent
       |
       v
Telegram Send Message
```

### Agent Components

| Component | Responsibility |
|---|---|
| Telegram Trigger | Receives customer messages |
| AI Agent | Understands messages, collects information, and determines the next step |
| OpenRouter Chat Model | Understands natural language and generates responses |
| Simple Memory | Maintains conversation context |
| Google Sheets Tool | Adds customer data after all saving conditions are met |
| Telegram Send Message | Sends the agent's response to the customer |

## 📥 Inputs and Outputs

### Inputs

- Customer messages through Telegram.
- Requested property type.
- Request type: Buy or Rent.
- Condition of the property to be purchased, when applicable.
- Customer's answer to the First Ourcase field, when applicable.
- Expected timeline.
- Budget.
- Customer name.
- Email address.
- Phone number.
- Customer corrections and confirmation of the final summary.

### Outputs

- Welcome messages and interactive responses through Telegram.
- Follow-up questions to collect missing information.
- Clarification requests for ambiguous answers.
- A final summary containing the nine required fields.
- A new row in Google Sheets after confirmation and fulfillment of the saving conditions.
- A message communicating the saving result after the operation has been verified.

## 📝 Final Summary and Customer Confirmation

After all information has been collected and validated, the agent must present a summary containing the nine fields in the following order:

```text
Property type:
Buy/Rent:
New/Resale:
First Ourcase:
Timeline:
Budget:
Name:
Email:
Phone Number:
```

The summary must contain the actual values provided by the customer, while applying the appropriate conditional rules.

If the customer corrects any information, the system must update it, present a new summary, and request confirmation again.

Completing all required fields is not sufficient to execute the saving operation. Explicit customer confirmation of the final summary is required.

## 🔐 Security and Action Execution Control

The project focuses on controlling the use of external tools, particularly the Google Sheets tool.

The system design must ensure:

- Data is not saved when required information is missing.
- Data is not saved when values are invalid or unclear.
- Data is not saved before explicit customer confirmation.
- Confirmation is requested again whenever the summary is modified.
- The tool's result is verified before announcing successful data storage.
- Reprocessing the same request is tested to prevent duplicate rows.
- Each customer's data is isolated from other customers' conversations.

Relying solely on System Prompt instructions is not sufficient to prevent premature data saving. The workflow design and tool execution controls must also be reviewed.

It is also necessary to verify that data has not actually been saved by reviewing the n8n execution logs and the contents of Google Sheets.

## 🧪 Testing and Validation

The following tests should be performed to verify the system's actual behavior:

| Test Case | Expected Result |
|---|---|
| Starting a new conversation | Send a welcome message and begin collecting information |
| Providing multiple details in one message | Use clearly provided information without repeating questions |
| Providing incomplete information | Ask only about the missing fields |
| Providing an ambiguous answer | Request clarification instead of guessing |
| Requesting to rent a property | Set both conditional fields to `Not Applicable` without asking about them |
| Sending consecutive messages | Maintain conversation context |
| Correcting an answer | Update the information and present a new summary |
| Completing all fields without confirmation | Do not execute the saving operation |
| Confirming the summary | Save the data in the correct columns |
| Google Sheets failure | Inform the customer of the failure without claiming success |
| Reprocessing the same request | Test duplicate-row prevention |
| Conversations with two different customers | Maintain independent customer data |

## 📦 Project Deliverables

The final delivery includes:

1. **n8n Workflow:** The complete workflow and its required components.
2. **System Prompt:** Agent instructions, data collection rules, validation rules, and tool usage conditions.
3. **Google Sheets:** A functional spreadsheet containing the nine specified columns.
4. **Test Results:** Documentation of actual test results and issues that have been addressed.
5. **Short Practical Demonstration:** Demonstrates information collection, customer confirmation, data storage, and result verification.

## 📈 Project Success Criteria

The project is considered successful when the agent can:

- Understand customer messages and collect the required information.
- Maintain conversation context and use previous answers.
- Identify missing information and validate values.
- Correctly apply purchase and rental rules.
- Update information when customers correct their answers.
- Request explicit confirmation before saving data.
- Save confirmed data in the specified columns.
- Verify the saving result before informing the customer that the operation was successful.
- Maintain independent customer sessions.
- Prevent duplicate storage of completed requests or manage it appropriately.

## 🚀 Potential Future Improvements

- Strengthen the mechanism for preventing duplicate data storage.
- Improve handling of ambiguous budgets and timeline answers.
- Enhance error handling for Google Sheets operations.
- Improve documentation of saving operations and their results.
- Expand tests related to memory, confirmation, and data correction.
- Improve agent instructions and tool usage controls based on test results.

## 📚 Conclusion

XYZ Real Estate AI Agent is a practical implementation of an AI-powered agent built using n8n. It combines natural language understanding, conversational memory, business rules, data validation, customer confirmation, and external tool execution.

The goal is not simply to connect an AI model to Google Sheets. It is to build an agent that understands the required information, determines the appropriate next step, follows clearly defined action execution conditions, and verifies the results before informing the customer.

**Core Principle:** Collect information accurately, validate it carefully, obtain explicit confirmation, execute actions under clear controls, and only report results that have been verified.

[Project Workflow](./Json/cs4kFYgWiyMJxGHH-XYZ_Real_Estate_AI_Agent.json)
