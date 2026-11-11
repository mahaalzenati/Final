
# Daleel — دليل | AI-Powered Enterprise Document Assistant Using RAG

[English](README.md) | [العربية](README.ar.md)

Daleel is an AI-powered assistant built using Dify and Retrieval-Augmented Generation (RAG), designed to help employees access information contained in enterprise documents and answer questions based on document content and its sources.

## 📌 Project Overview

**Daleel** is an intelligent assistant that allows employees to ask questions about contracts, meeting minutes, and appendices. It retrieves information relevant to each question from an enterprise knowledge base and uses a language model to generate clear answers grounded in the retrieved information.

The project focuses on improving information accessibility, distinguishing between officially documented information and proposed suggestions, and reducing answers that are not supported by evidence.

## 🎯 Problem Statement

Enterprise documents contain important information distributed across contracts, appendices, and meeting minutes. Finding specific information or verifying its accuracy can therefore be time-consuming.

Key challenges include:

- Difficulty finding a specific clause across multiple documents.
- The need to extract financial amounts, payment terms, and delivery dates.
- The possibility of confusing information from different contracts.
- The risk of treating suggestions mentioned in meeting minutes as officially approved decisions.
- The need to verify the source of an answer rather than relying on unsupported responses.

## 💡 Proposed Solution

Daleel provides a conversational interface for enterprise documents. Users can ask questions in natural language, and the system retrieves relevant document passages and uses them to generate an answer.

The assistant is designed to:

- Retrieve information from the knowledge base.
- Answer questions related to contracts and projects.
- Clarify contract values, financial amounts, and payment terms.
- Identify execution periods and delivery dates.
- Distinguish between suggestions and officially approved amendments.
- Ground responses in document content and identify their sources.
- Avoid guessing when the available evidence is insufficient.

## 👥 Target Audience

- Employees who work with enterprise documents.
- Project management teams.
- Employees responsible for tracking contracts and deadlines.
- Teams that need quick access to meeting decisions and agreement terms.

## ⚙️ Tools and Technologies

| Tool or Technology | Purpose |
|---|---|
| **Dify** | Building the AI assistant and configuring its workflow |
| **Knowledge Base** | Storing enterprise documents and making them available for retrieval |
| **Knowledge Retrieval** | Retrieving passages relevant to the user's question |
| **LLM (Large Language Model)** | Understanding the question and retrieved passages, then generating the answer |
| **RAG (Retrieval-Augmented Generation)** | Connecting document retrieval with answer generation |
| **Prompt Engineering** | Guiding the assistant to rely on sources and avoid unsupported assumptions |

## 🗂️ Knowledge Base

The project uses sample documents belonging to a fictional company named **Afaq Digital Solutions Company** (شركة آفاق للحلول الرقمية).

### 1. Contracts and Appendices

| Document | Content |
|---|---|
| `CON-001_عقد_تطوير_موقع.pdf` | Website development contract for Al Noor Store |
| `CON-002_عقد_نظام_المخزون.pdf` | Inventory management system contract for Al Madar Company |
| `CON-003_عقد_الصيانة_والدعم.pdf` | Maintenance and support contract for Al Noor Store |
| `ADD-001_ملحق_تعديل_مدة_التنفيذ.pdf` | Appendix modifying the project delivery date |

### 2. Meeting Minutes

| Document | Content |
|---|---|
| `MIN-001_اجتماع_بدء_مشروع_النور.docx` | Al Noor Store project kickoff meeting minutes |
| `MIN-002_اجتماع_متابعة_مشروع_النور.docx` | Al Noor Store project follow-up meeting minutes |
| `MIN-003_اجتماع_تأخير_التسليم.docx` | Meeting minutes discussing delivery delays |
| `MIN-004_اجتماع_مشروع_المخزون.docx` | Inventory management system project meeting minutes |

## 🔄 How the System Works

The system follows this logical workflow:

1. **Question Submission:** The user asks a question about a contract, project, or meeting.
2. **Knowledge Retrieval:** The Knowledge Retrieval node searches the knowledge base for passages relevant to the question.
3. **Answer Generation:** The language model uses the question, instructions, and retrieved passages to formulate a response.
4. **Response Delivery:** The assistant provides an answer based on the available information and references its source when available.

### Workflow Diagram

```text
User
  |
  v
Dify Workflow / Chatflow
  |
  v
Knowledge Retrieval
  |
  | Retrieve relevant passages
  v
LLM
  |
  | Generate an answer using retrieved information
  v
Answer with Supporting Information
```

## 🧠 Role of RAG

The project is based on combining information retrieval with answer generation.

- **Retrieval:** Searching the knowledge base for passages relevant to the question.
- **Augmented Context:** Providing the retrieved passages to the language model as context for generating the answer.
- **Generation:** Producing a natural-language response based on the question and available context.

This approach helps connect answers to document content instead of relying solely on the model's general knowledge.

However, using RAG does not guarantee that every answer is correct. The result also depends on retrieval quality, the relevance of retrieved passages, and how the final response is generated.

## 🧪 Testing and Validation

Project testing focuses on verifying the assistant's ability to retrieve the correct information from documents and use it accurately and consistently.

### Test Cases

| Test Type | Objective |
|---|---|
| Contract Information | Verify contract values and execution periods |
| Payment Terms | Verify payment percentages, amounts, and payment milestones |
| Delivery Dates | Distinguish between original and amended delivery dates |
| Relationships Between Documents | Verify that meeting minutes are linked to the correct contracts |
| Decisions and Suggestions | Distinguish between proposals and officially approved amendments |
| Missing Information | Verify that the assistant avoids guessing when evidence is unavailable |
| Retrieval Quality | Ensure that retrieved passages are relevant to the question |
| Answer Quality | Verify the accuracy, completeness, and consistency of answers with their sources |

### Example: Retrieval Accuracy Test

**Question:** Which contract is associated with the Al Noor Store project kickoff meeting minutes?

- **Expected Answer:** `CON-001`
- **Verification Source:** `MIN-001_اجتماع_بدء_مشروع_النور.docx`
- **Potential Failure Case:** Retrieving `CON-002` instead of `CON-001`.
- **What Needs to Be Reviewed:** The passages retrieved from the knowledge base, their relevance to the question, and how the language model uses them when generating the answer.

This example highlights the importance of examining the retrieved information itself rather than evaluating only the final response.

## 🔍 System Quality Evaluation

Daleel's performance can be evaluated through several dimensions:

- **Retrieval Relevance:** How relevant the retrieved passages are to the question.
- **Accuracy:** The correctness of the information in the answer.
- **Groundedness:** The extent to which the answer is supported by document content.
- **Source Attribution:** How clearly the information source is identified.
- **Consistency:** Whether the answer is consistent with other relevant documents.
- **Decision Status:** Whether suggestions are correctly distinguished from approved decisions.
- **Uncertainty Handling:** How appropriately the system handles missing or insufficient evidence.

### Improvement Cycle

1. Submit a test question.
2. Review the retrieved passages.
3. Compare the answer with the original document content.
4. Identify the type of issue: irrelevant retrieval, inaccurate answer, or insufficient grounding.
5. Adjust settings or instructions when necessary.
6. Retest to verify improvement.

## 🛡️ Reliability and Limitations

The project focuses on making answers traceable to their sources while following these principles:

- Do not invent clauses, amounts, or dates that do not exist in the documents.
- Do not confuse contracts belonging to different projects.
- Do not treat suggestions as official decisions without evidence of approval.
- Clearly indicate when the available information is insufficient to support a specific answer.
- Review the source of information when documents or retrieved results contain conflicting information.

## 📈 Project Success Criteria

The system can be considered more reliable when it can:

- Retrieve the correct passages relevant to a question.
- Provide accurate answers about contracts, financial amounts, and dates.
- Link meeting minutes to the correct contracts.
- Distinguish between original and amended delivery dates.
- Distinguish between suggestions and officially approved amendments.
- Identify the sources of information.
- Avoid guessing when evidence is insufficient.
- Demonstrate verifiable improvement after retrieval or answer-generation issues are addressed.

## 🚀 Potential Future Improvements

- Improve retrieval settings to increase the relevance of retrieved passages.
- Improve document organization and divide content into more suitable chunks.
- Review document metadata to make documents easier to distinguish.
- Develop a more comprehensive test set covering direct questions, alternative question wording, and questions requiring comparisons across multiple documents.
- Improve instructions that guide the model to rely on evidence.
- Document test results before and after improvements.

## 📚 Conclusion

**Daleel** is a practical application of RAG using Dify, designed to make enterprise information easier to access by turning documents into a knowledge source that users can query using natural language.

The project combines a knowledge base, relevant passage retrieval, answer generation, and verification of responses against original documents.

**Core Principle:** An answer is not reliable simply because it sounds correct. It is essential to verify that the retrieved information belongs to the appropriate document, that the answer accurately reflects its content, and that every mentioned decision or amendment is supported by a reliable source.

---

## 📎 Project Link

- **Live Application:** [Daleel — Try the Assistant](https://udify.app/chat/28rgAdgo0M3yyADB)
