
# TECHFIX — Smart Computer Troubleshooting Assistant

[English](README.md) | [العربية](README.ar.md)

TECHFIX is an AI-powered assistant that helps users understand common computer problems and receive clear, safe initial guidance using a technical knowledge base powered by Retrieval-Augmented Generation (RAG).

## 📌 Project Overview

**TECHFIX** is an AI assistant built using the Dify platform. It aims to simplify computer troubleshooting by retrieving relevant information from a specialized knowledge base and using a language model to generate an appropriate response.

The project focuses on providing guidance based on available information, requesting additional details when necessary, and clearly communicating the limitations of the assistance when sufficient knowledge is unavailable.

## 🎯 Problem Statement

Users often struggle to understand the causes of computer problems and find clear, appropriate technical guidance, especially when information is complex or scattered across multiple sources.

The project covers common issues such as:

- Slow computer performance.
- Insufficient storage space.
- Internet and Wi-Fi connectivity problems.
- The need for clear and safe technical guidance.

## 💡 Proposed Solution

TECHFIX provides an assistant that allows users to describe their computer problems in Arabic. The system then retrieves relevant information from its knowledge base and uses it to generate an appropriate response.

Its main functions include:

- Retrieving technical information relevant to the reported problem.
- Providing clear and structured initial guidance.
- Requesting additional details when the problem description is insufficient.
- Indicating when the available knowledge is insufficient.
- Considering safety and warning users when a problem requires a qualified technician.

## 👥 Target Audience

- Computer users.
- Students and beginners in technology.
- People experiencing computer performance, storage, or internet connectivity problems.
- Users who need simplified technical guidance in Arabic.

## ⚙️ Technologies and Concepts

- **Dify:** Building the AI assistant application and managing its components.
- **Knowledge Base:** Organizing technical information into specialized documents.
- **RAG (Retrieval-Augmented Generation):** Connecting answer generation with information retrieved from the knowledge base.
- **Knowledge Retrieval:** Searching for content relevant to the user's question.
- **LLM (Large Language Model):** Generating responses based on the question, instructions, and retrieved context.
- **Prompt Engineering:** Defining the assistant's role, response rules, and limitations.
- **Document Processing:** Preparing documents for effective retrieval.
- **Chunking:** Splitting content into segments while preserving meaning and context.
- **Grounding:** Evaluating whether the retrieved information supports the claims made in the generated response.

## 🔄 How the System Works

1. **Question Submission:** The user describes the computer problem they are experiencing.
2. **Knowledge Retrieval:** The system searches the knowledge base for content related to the reported problem.
3. **Answer Generation:** The language model uses the question, instructions, and retrieved information to generate a response.
4. **Response Delivery:** The assistant provides guidance to the user and explains knowledge limitations when necessary.

## 🗂️ Knowledge Base

The knowledge base consists of four specialized documents:

| Document | Content |
|---|---|
| `01-بطء-الحاسوب.md` | Performance issues, possible causes of slow computers, and troubleshooting steps. |
| `02-مساحة-التخزين.md` | Causes of insufficient storage space, ways to check storage usage, and possible solutions. |
| `03-اتصال-الإنترنت.md` | Network and connectivity problems and initial diagnostic questions. |
| `04-السلامة-وحدود-المساعدة.md` | Safety guidelines, warnings, and situations that require a qualified technician. |

## 🧠 Role of Artificial Intelligence

The project uses AI to retrieve technical knowledge and generate guidance appropriate to the user's question.

The assistant follows these principles:

- Do not invent information or unsupported troubleshooting steps.
- Do not confirm the cause of a problem without sufficient information.
- Request additional details when necessary.
- Clearly communicate knowledge limitations when relevant information is unavailable.
- Avoid instructions that could cause data loss or damage the system.
- Refer users to a qualified technician when the problem exceeds the assistant's scope.

> **Note:** TECHFIX is a technical guidance assistant. It does not physically inspect computers or perform repairs directly.

## 🧪 Testing and Improvement

Initial testing showed that the assistant can provide useful guidance for some cases, but the level of detail and completeness is not consistent across all responses.

In one internet connectivity scenario, the response was limited despite retrieving information related to the topic.

This case highlights the importance of evaluating two separate stages:

- **Retrieval Quality:** How relevant and sufficient is the retrieved information?
- **Answer Quality:** How accurate, clear, complete, and well-supported is the final response?

### Evaluation Criteria

The evaluation process considers the following criteria:

| Criterion | Description |
|---|---|
| **Relevance** | How closely the retrieved results relate to the user's question. |
| **Correctness** | Accuracy of the information and suggested steps. |
| **Groundedness** | Whether the response is supported by the retrieved knowledge. |
| **Completeness** | Whether the response provides sufficient information. |
| **Clarity** | How clear and understandable the guidance is. |
| **Safety** | Whether the instructions follow appropriate safety considerations. |
| **Uncertainty Handling** | How appropriately the assistant handles insufficient information. |

### Improvement Plan

1. Test direct questions covering the knowledge base.
2. Test different ways of describing the same problem.
3. Test questions that are not covered by the knowledge base.
4. Test incomplete questions and out-of-scope questions.
5. Review retrieved results and evaluate the final response.
6. Identify the cause of failures and improve the system.
7. Retest to verify the effectiveness of improvements.

## 🛡️ Safety and Limitations

The project recognizes that technical guidance can affect users' data and computer systems. Therefore, the assistant follows these guidelines:

- Avoid providing steps that are not supported by the available information.
- Explain warnings before suggesting sensitive actions.
- Avoid making definitive conclusions when information is insufficient.
- Clearly state when the available knowledge is not sufficient.
- Refer users to a qualified specialist when the problem exceeds the assistant's scope.

## 📈 Project Success Criteria

The project is evaluated based on the assistant's ability to:

- Retrieve relevant information from the knowledge base.
- Provide responses related to the reported problem.
- Maintain the accuracy of source-based information.
- Request additional details when necessary.
- Communicate knowledge limitations when relevant information is unavailable.
- Provide clear and safety-conscious guidance.
- Handle questions outside its scope appropriately.
- Achieve measurable and verifiable improvements after modifications.

## 🚀 Potential Future Improvements

- Improve document quality and divide content into retrieval-friendly chunks.
- Optimize retrieval settings to reduce irrelevant results.
- Develop a more comprehensive test set to evaluate answer quality.
- Improve the instructions used to guide the language model.
- Reevaluate system performance after every significant modification.

## 📚 Conclusion

TECHFIX represents a practical application of building an AI assistant that relies on a specialized knowledge base to provide technical guidance in Arabic.

The project combines knowledge organization, information retrieval, answer generation, result quality evaluation, failure analysis, and system improvement based on testing.

**Core Principle:** Generating an answer is not enough. The relevance of the information used, the accuracy and completeness of the response, and the limitations of the assistance provided must also be evaluated.

## 📎 Project Link

- **Live Application:** [TECHFIX — Try the Assistant](https://udify.app/chat/XezHChK9hk2hImTH)
