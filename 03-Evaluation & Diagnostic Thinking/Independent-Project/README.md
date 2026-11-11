
# Tajarob — تجارب

[English](README.md) | [العربية](README.ar.md)

Tajarob is an Arabic-language technical platform that helps developers and students share programming problems, discover solutions from other people's experiences, and document whether suggested solutions have been successful.

## 📌 Project Overview

Tajarob aims to build a technical community where programming questions, problems, and answers are gathered in one place. This allows users to benefit from previous experiences instead of searching across scattered websites and discussions.

The platform focuses on organizing technical problem details, finding semantically similar questions, and tracking the results of solutions shared by users.

## 🎯 Problem Statement

Developers and students face several challenges when trying to solve technical problems:

- Solutions and information are scattered across different websites and sources.
- Finding similar questions can be difficult when the problem is described using different wording.
- Some questions lack important technical details, such as error messages, development environments, and previously attempted steps.
- It is not always clear whether a suggested solution has actually been tested or worked.
- Users repeatedly search for solutions to problems that others may have already encountered.

## 💡 Proposed Solution

Tajarob provides an interactive space for sharing programming problems and answers, using AI to help discover semantically similar questions and improve question descriptions.

The platform allows users to:

- Publish technical questions with problem details and error messages.
- Search previous questions based on semantic similarity.
- Add answers and mark an accepted answer.
- Document the results of testing suggested solutions.
- Save important questions and return to them later.
- Track their questions, answers, and notifications through a personal dashboard.

## 👥 Target Audience

- Software developers.
- Programming students and beginners.
- Web and mobile application developers.
- DevOps and infrastructure professionals.
- Users who encounter problems related to databases, APIs, hosting, and development tools.

## ⚙️ How It Works

1. **Account Registration:** The user creates an account or logs in.
2. **Explore Questions:** The user browses published questions and searches by keywords, categories, or semantic similarity.
3. **Post a Question:** The user provides a problem title, description, and available technical details, such as error messages, development environment, and previously attempted steps.
4. **Suggest Similar Questions:** The system analyzes the question and searches for questions with similar meanings using semantic embeddings.
5. **Continue Publishing:** The user can review similar results or continue publishing their question without being forced to cancel it.
6. **Share Solutions:** Users add answers, and the question owner can select an accepted answer.
7. **Track Results:** The solution testing status is recorded as not tested, tested successfully, or unsuccessful.
8. **Track Activity:** Users can save questions and follow their questions, answers, and notifications through their accounts.

## 🧠 Role of Artificial Intelligence

AI is intended to support technical search and information organization, not replace users' expertise or automatically determine whether a solution is correct.

The planned AI capabilities include:

- **Semantic Search:** Converting question content into numerical embeddings and comparing them through vector search to find questions with similar meanings, even when different words are used.
- **Question Improvement:** Suggesting clearer titles, identifying missing technical information, and recommending relevant categories and tags.
- **Knowledge Discovery:** Displaying similar questions, their answers, and solution testing results recorded in the database.

### AI Usage Guidelines

- A solution should not be considered correct simply because AI suggested or displayed it in search results.
- The system must not generate answers or search results that do not exist in the database.
- An answer is considered successful only when the user reports a successful testing result.
- Question content must not be modified automatically without the owner's approval.
- Sensitive AI operations must be handled on the server, with API keys securely protected.

## 🔄 Automation and Processes

The project connects the user interface to a database and backend services to support the following operations:

- Creating user accounts and managing login sessions.
- Saving, retrieving, updating, and deleting questions and answers according to permissions.
- Generating embeddings for new questions and updating them when needed.
- Searching for similar questions using the database and vector search.
- Updating question status when an answer is accepted, according to system rules.
- Saving bookmarked questions and managing in-platform notifications.
- Tracking question and solution statuses and displaying them to users.

## 📥 Inputs and Outputs

### Inputs

- Account registration and login information.
- Question title and problem description.
- Expected and actual behavior.
- Error message or stack trace, when available.
- Programming language, framework, or development environment.
- Previously attempted steps.
- Optional category, tags, and code snippets.
- User answers and solution testing results.

### Outputs

- A list of published technical questions.
- Search results and semantically similar questions.
- Answers, accepted solutions, and user-reported testing results.
- Suggestions for improving question descriptions and categorization.
- A list of saved questions.
- Notifications related to activity within the platform.
- A personal dashboard displaying the user's questions, answers, and activity.

## 🛠️ Tools and Technologies

According to the project requirements:

| Technology | Purpose |
|---|---|
| **Lovable** | Application development |
| **Supabase Auth** | Authentication and session management |
| **Supabase PostgreSQL** | Storing user, question, and answer data |
| **PostgreSQL pgvector** | Storing embeddings and performing vector search |
| **Supabase Edge Functions** | Secure backend operations for AI and search |
| **Embeddings Service** | Converting text into numerical representations for semantic search |
| **Supabase Row Level Security (RLS)** | Applying data access policies based on user permissions |

## 🔐 Security and Data Protection

The project requires security measures that include:

- Protecting pages and operations that require authentication.
- Applying RLS policies to application tables.
- Allowing users to manage their own profiles, questions, and answers according to defined permissions.
- Preventing users from modifying other users' records.
- Validating record ownership and input data on the server.
- Protecting AI service API keys from exposure in the frontend.
- Restricting access to embedding generation and vector search operations.
- Preventing unauthorized notification creation.
- Protecting profile images when file storage is used.

> Listing these security requirements in the project description does not, by itself, mean that all security policies have been implemented and tested.

## 🗄️ Database Design

The proposed database design includes the following tables:

| Table | Purpose |
|---|---|
| `profiles` | User profile information |
| `categories` | Technical categories |
| `questions` | Published questions and problems |
| `answers` | User-submitted answers |
| `saved_questions` | Saved questions |
| `notifications` | In-platform notifications |
| `question_embeddings` | Embeddings used for semantic search |

The design also requires clear relationships between tables, constraints to prevent multiple accepted answers for the same question, indexes to improve query performance, and appropriate access policies.

## 🧪 Testing and Validation

The core Tajarob platform features were tested to verify user and data management, question publishing, input validation, and the handling of discovered issues.

### Test Results

| Test Case | Result | Details |
|---|---|---|
| Account Registration and Login | Pass | An account was successfully created, and the user logged in. |
| Logout and Login Again | Pass | The user logged out, refreshed the page, and logged in again while retaining their data. |
| User Data Protection | Pass | Neither of the two test accounts could access the other account's data. |
| Publish a New Question | Pass | The question was successfully published and remained available after refreshing the page. |
| Search for Similar Questions | Issue Found and Fixed | Initial suggestions were unrelated to the problem. The issue was addressed using Lovable, and the functionality was tested again. |
| Prevent Publishing a Question Without a Description | Pass | The system rejected the submission and displayed a validation message indicating that the text must be longer. |
| Short Description Validation | Pass | A message indicating that the description was too short was displayed. |
| Prevent Users from Answering Their Own Questions | Issue Found and Fixed | Users were initially able to answer their own questions. The issue was addressed, and related functionality was tested again. |
| Distinguish Between Empty and Short Descriptions | Issue Found and Fixed | The validation messages were corrected, and related functionality was tested again according to the documented test results. |

### Issue Resolution and Retesting

After issues were discovered during the initial tests, Lovable was used to make the necessary changes.

The related functionality was then tested again to verify the fixes. Regression testing was also performed to ensure that other features related to the changes were not affected.

**Result:** According to the documented test results, the identified issues were addressed, and the related functionality was retested.

### Testing Evidence

- **Account Registration:** [View Evidence](./Screenshots/0.png)
- **User Data Protection:** [View Evidence](./Screenshots/4.png)
- **Publishing and Saving a Question:** [View Evidence](./Screenshots/1%282%29.png)
- **Adding an Answer:** [View Evidence](./Screenshots/3%282%29.png)
- **Discovered Issues:** [Screenshot 1](./Screenshots/5.png) · [Screenshot 2](./Screenshots/6.png) · [Screenshot 3](./Screenshots/2%282%29.png)
- **Retesting After Fixes:** [Screenshot 1](./Screenshots/7.png) · [Screenshot 2](./Screenshots/9.png) · [Screenshot 3](./Screenshots/8.png)

## ⚠️ Potential Challenges

- **Different Problem Descriptions:** Finding questions with similar meanings requires genuine semantic search rather than relying only on keyword matching.
- **Search Result Accuracy:** The embedding model, similarity threshold, and result limits need to be configured and the actual quality of results evaluated.
- **Data Protection:** Supporting multiple users requires properly configured access policies at the database and backend levels.
- **Technical Content Formatting:** Code snippets and English error messages must remain readable and properly formatted within an Arabic interface.
- **Documenting Solution Success:** The system must distinguish between a suggested answer and a result confirmed by the user after testing.

## 📚 What Can Be Learned from This Project

This project provides practical experience with:

- Building a web application using React and TypeScript.
- Connecting a frontend to a real database.
- Managing authentication and user permissions.
- Designing relational databases using PostgreSQL.
- Applying Row Level Security (RLS) policies.
- Understanding semantic search, embeddings, and vector search.
- Integrating AI services through secure backend functions.
- Designing an Arabic user experience that supports RTL and mixed technical content.
- Handling errors and validating results instead of assuming operations have succeeded.

## 🚀 Potential Future Improvements

- Improve search result ranking based on relevance and solution quality.
- Add a rating system to help users discover useful answers.
- Improve category and tag suggestions.
- Add advanced moderation tools when needed.
- Enhance search with more detailed technical filters.
- Expand security and performance testing.
- Add email notifications in the future if needed.

## 📎 Project Links

- **Live Application:** [Tajarob](https://screenshot-heartbeat.lovable.app)
- **GitHub Repository:** [Final](https://github.com/mahaalzenati/Final)

## 👩‍💻 Author

**Maha Alzenati**

[LinkedIn](https://www.linkedin.com/in/maha-alzenati-gamedev/) · [GitHub](https://github.com/mahaalzenati)
