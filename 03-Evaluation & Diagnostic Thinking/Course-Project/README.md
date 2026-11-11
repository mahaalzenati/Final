
# TaskBridge

[English](README.md) | [العربية](README.ar.md)

> A web application that helps freelancers and early-career professionals transform unclear work requests into organized plans, create and manage tasks, track progress, and save plans for future reference.

---

## 🎯 Problem

### Context

Freelancers and early-career professionals receive work requests that may include multiple goals and requirements without being clearly divided into tasks and actionable steps.

### Problem

Users may find it difficult to organize work requirements, identify tasks and their priorities, and track progress toward achieving the desired outcome.

### Why Does Solving This Problem Matter?

Organizing work into clear plans and tasks helps improve time management, set priorities, track completion, and reduce the likelihood of forgetting tasks or overlooking important requirements.

---

## 💡 Solution

**TaskBridge** provides a work plan management application that allows users to create and save plans, divide work into tasks, set priorities and execution statuses, and track progress through an organized interface.

### What Does the System Do?

1. Allows users to create an account and log in to access their personal plans.
2. Allows users to create a work plan containing a title, description, goal, and optional deadline.
3. Allows users to add, edit, and delete tasks, as well as set their priorities and execution statuses.
4. Automatically calculates the progress percentage based on the number of completed tasks compared to the total number of tasks.
5. Saves plans and tasks in a database so users can access them after reloading the page.

---

## 👤 Users

### Primary Users

- Freelancers.
- Early-career professionals.

### User Needs

- Transforming work requirements into clear plans.
- Dividing work into actionable tasks.
- Setting priorities and tracking task statuses.
- Knowing the progress percentage of each plan.
- Saving plans and tasks and accessing them later.

---

## 🧠 How Was the Solution Designed?

I designed TaskBridge with a focus on the core functions of work management, avoiding unnecessary features in the initial version.

- **Organized Plans:** Each plan includes a title, description, goal, and optional deadline.
- **Task Management:** The ability to add, edit, and delete tasks, as well as change their priorities and statuses.
- **Progress Tracking:** Automatically calculating the completion percentage instead of entering it manually.
- **Data Persistence:** Using Supabase to permanently store plans and tasks.
- **User Privacy:** Using authentication and database security policies to ensure that each user can access only their own data.
- **Limited Scope:** AI-powered plan generation is not included in this version.

---

## ⚙️ How Does the System Work?

```text
Log In
   ↓
View Saved Plans
   ↓
Create a Work Plan
   ↓
Enter Title, Description, and Goal
   ↓
Save Plan to Supabase
   ↓
Add and Organize Tasks
   ↓
Update Priorities and Task Statuses
   ↓
Automatically Calculate Progress
   ↓
Save Changes and Access Them Later
```

---

## 🤖 Role of Artificial Intelligence

### What Is the Role of AI in This Project?

This version does not include AI-powered plan or task generation.

The system relies on information entered by the user to create plans and manage tasks, while the progress percentage is calculated using predefined programmatic logic.

### What Should AI Not Do?

- Claim to generate plans or tasks using AI when no AI service is integrated.
- Display artificially generated content as if it were the result of actual analysis.

---

## 🔄 Automation

The system automatically performs the following operations:

- Loads the saved plans belonging to the currently logged-in user.
- Saves plans and tasks to the database when save operations succeed.
- Updates the user interface after successful create, edit, and delete operations.
- Calculates the progress percentage of each plan based on task statuses.
- Deletes tasks associated with a plan when that plan is deleted, according to the relationship defined in the database.

---

## 🗂️ Data

### Inputs

**Plan Data:**

- Plan title.
- Work description.
- Goal to be achieved.
- Deadline (optional).

**Task Data:**

- Task title.
- Task description (optional).
- Priority: High, Medium, or Low.
- Status: Not Started, In Progress, or Completed.

**Account Data:**

- Email address and password when creating an account or logging in, according to Supabase Auth settings.

### Outputs

- A list of the user's saved plans.
- Details of each plan and its associated tasks.
- Total number of tasks and number of completed tasks.
- Automatically calculated progress percentage.
- Loading, success, and error states that help users understand the result of each operation.

If a plan does not contain any tasks, its progress percentage is **0%**.

---

## 🛠️ Tools and Technologies

| Tool | Purpose |
|---|---|
| Lovable | Building and developing the application interface |
| Supabase Auth | Account creation, login, and session management |
| Row Level Security (RLS) | Restricting data access according to user ownership |

---

## 🔑 Key Design Decisions

### Decision 1: Using a Persistent Database

**Decision:**

Using Supabase to store plans and tasks instead of relying on sample data or frontend state alone.

**Reason:**

Allowing users to return to their plans after refreshing the page while preserving saved data.

### Decision 2: Applying Security at the Database Level

**Decision:**

Using Supabase Auth for authentication and enabling Row Level Security policies on the plans and tasks tables.

**Reason:**

Ensuring that users cannot read, modify, or delete another user's data, even if they attempt to bypass frontend validation.

### Decision 3: Automatically Calculating Progress

**Decision:**

Calculating the progress percentage by dividing the number of completed tasks by the total number of tasks.

**Reason:**

Providing an indicator that reflects actual completion status instead of relying on a percentage manually entered by the user.

---

## 🧪 Testing

### Test 1: Creating and Saving a Plan

**Input:**

A plan title, work description, and goal, with an optional deadline.

**Expected Result:**

The plan should be saved in Supabase and appear in the user's plans, remaining available after reloading the page.

**Actual Result:**

The plan was saved in the database and appeared in the user's personal plans.

**Status:** ✅ Pass

### Test 2: Calculating Plan Progress

**Input:**

Creating a plan containing four tasks, then changing the status of two tasks to "Completed".

**Expected Result:**

Displaying a progress percentage of 50%.

**Actual Result:**

The calculated progress percentage was displayed.

**Status:** ✅ Pass

---

## 📸 Evidence

### Final Result

Add a screenshot of the application's final interface after verifying it.

![Final Result](./screenshots/final-result.png)

---

## ⚠️ Potential Challenges

- Ensuring that each task is associated with the correct plan and its owning user.
- Protecting plans and tasks from unauthorized access.
- Maintaining accurate progress percentages when tasks are added, their statuses are changed, or they are deleted.
- Handling save errors without displaying incorrect success messages.

### How to Address Them

- Enforcing ownership relationships and appropriate constraints in the database.
- Applying RLS policies and validating access permissions.
- Calculating progress using actual task data.
- Testing success and failure scenarios and avoiding reporting success before receiving database confirmation.

These are targeted design solutions, and their implementation and practical effectiveness should be verified.

---

## 📚 What I Learned

### Technical Lesson

The importance of connecting the user interface to a persistent database and understanding the relationship between authentication, access permissions, and data storage.

### Problem-Solving Lesson

Defining a clear scope for the initial version helps focus on core functions, such as creating plans, managing tasks, and tracking progress, instead of adding unnecessary features.

### AI Lesson

Not every work management application needs to use artificial intelligence. A useful solution can be built using clear programmatic logic, with the possibility of adding AI in the future if there is an actual need for it.

---

## 🔮 Future Improvements

If I continue developing this project, I plan to:

- Add an optional feature for generating a draft work plan using AI.
- Improve task sorting and organization based on priority.
- Develop a visual representation of progress across different plans.
- Add automated tests covering core operations and security policies.
- Improve the user experience across mobile devices and different screen sizes.

These are proposed future improvements and are not confirmed features of the current version.

---

## 🔗 Project Links

- **Live Demo:** [TaskBridge](https://pixel-perfect-showcase-8134.lovable.app)
- **GitHub Repository:** [Add Repository Link]

---

## 👩‍💻 Project Author

**Maha Alzenati**

- **LinkedIn:** [Add Your LinkedIn Profile]
- **GitHub:** [Add Your GitHub Profile]

---
