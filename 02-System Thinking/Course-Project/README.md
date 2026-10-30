
# SkillBridge Lite

[English](README.md) | [العربية](README.ar.md)

> A web application that helps students, recent graduates, and early-career professionals understand how well their skills, projects, and experience align with the requirements of a specific career opportunity, and identify areas they can improve.

---

## 🎯 Problem

### Context

Students and recent graduates explore internship and job opportunities, but they may not know how well their current skills, projects, and experience align with the requirements of each opportunity.

### Problem

Beginners may find it difficult to identify which skills are relevant to a specific opportunity, recognize requirements that are not covered by their current qualifications, and determine appropriate steps to improve their career readiness.

### Why Does This Problem Matter?

Understanding the relationship between a person's current capabilities and the requirements of career opportunities helps them make more informed career decisions and identify learning and development priorities.

---

## 💡 Solution

**SkillBridge Lite** provides a simple interface that allows users to document their professional profiles, explore specific career opportunities, review their requirements, and access a dedicated interface for analyzing their compatibility.

### What Does the System Do?

1. Allows users to enter and edit their professional profile information.
2. Displays career opportunities across various technical fields.
3. Displays details of each opportunity, including its description, required skills, and responsibilities.
4. Provides a compatibility analysis interface that displays relevant skills, potential gaps, and recommended next steps.

---

## 👤 Users

### Primary Users

- University students.
- Recent graduates.
- Early-career professionals.

### Their Needs

To understand how their documented skills, projects, and experience relate to a specific career opportunity and identify areas that need improvement.

---

## 🧠 How Was the Solution Designed?

I designed the application around a clear user journey that starts with documenting the professional profile, followed by exploring opportunities and reviewing the details of a selected opportunity, and finally accessing the compatibility analysis interface.

- **Professional Profile-Based Analysis:** Ensuring that the analysis uses the current profile data and the selected opportunity.
- **Simple Navigation:** Dividing the application into five main interfaces.
- **Organized Results:** Displaying relevant skills, potential gaps, and next steps.
- **Transparency:** Distinguishing between actual analysis results and illustrative examples.

---

## ⚙️ How Does the System Work?

```text
Professional Profile
        ↓
Explore Career Opportunities
        ↓
Select an Opportunity
        ↓
View Details and Requirements
        ↓
Request Compatibility Analysis
        ↓
Use Professional Profile and Opportunity Requirements
        ↓
AI Analysis
        ↓
Relevant Skills
Potential Gaps
Next Steps
```

---

## 🤖 Role of Artificial Intelligence

### Intended Functions

- Compare the user's skills, projects, and experience with the requirements of the selected opportunity.
- Identify information in the professional profile that is relevant to the opportunity.
- Highlight potential gaps between the professional profile and the requirements.
- Suggest practical steps for professional development.

### What Should It Not Do?

- Fabricate skills, qualifications, projects, or experience.
- Claim to have performed an actual analysis without successfully executing it.
- Treat potential gaps as conclusive evidence that the user is unqualified.
- Guarantee that the user will get a job or internship opportunity.

---

## 🔄 Automation

- Update the professional profile interface when data is edited within the application state.
- Navigate between interfaces and display the details of the selected opportunity.
- Navigate to the compatibility analysis interface using the current profile and selected opportunity.
- Display loading, missing data, service unavailability, and error states.

---

## 🗂️ Data

### Inputs

- Name and professional title.
- Personal summary.
- Skills, projects, and experience.
- Selected career opportunity and its requirements.

### Outputs

- Details of the selected opportunity.
- Relevant skills.
- Potential gaps.
- Suggested steps for professional development.

---

## 🛠️ Tools and Technologies

| Tool | Purpose |
|---|---|
| Lovable | Building the application interface and developing the prototype |

---

## 🧪 Testing

### Test 1: Editing the Professional Profile

- **Input:** Entering professional profile information and saving the changes.
- **Expected Result:** Updating the profile information within the application.
- **Actual Result:** The information was updated and the new data was saved.
- **Status:** ✅ Pass

### Test 2: Browsing a Career Opportunity

- **Input:** Selecting the AI Automation Intern opportunity.
- **Expected Result:** Displaying the company name, description, required skills, responsibilities, and compatibility analysis button.
- **Actual Result:** All details of the selected opportunity were displayed.
- **Status:** ✅ Pass

### Test 3: Requesting Compatibility Analysis

- **Input:** Selecting an opportunity and clicking the compatibility analysis button.
- **Expected Result:** Performing the analysis.
- **Actual Result:** The analysis was executed and the expected results were displayed.
- **Status:** ✅ Pass

---

## 📸 Evidence

### Final Results

| Test | Screenshot |
|---|---|
| Test 1 | [View Screenshot](./Screenshots/Test1.png) |
| Test 2 | [View Screenshot](./Screenshots/Test1.1.png) |
| Test 3 | [View Screenshot](./Screenshots/Test1.2.png) |

---

## ⚠️ Potential Challenges

- Handling empty or incomplete professional profiles.
- Ensuring that the correct opportunity and current profile are used in the analysis.
- Avoiding displaying results that suggest an actual analysis has been performed when the service is unavailable.
- Ensuring ease of use across mobile devices and different screen sizes.

### Suggested Solutions

- Testing missing-data scenarios and displaying clear messages.
- Verifying data transfer between interfaces.
- Separating actual analysis from illustrative examples.
- Testing the design across different screen sizes.

---

## 📚 What I Learned

### Technical Lesson

The importance of managing application state and organizing navigation between interfaces to ensure that core features work together without unnecessary technical complexity.

### Problem-Solving Lesson

Transforming a general career-related problem into a defined user journey helps control the scope of the solution and focus on the most important features.

### AI Lesson

Having a dedicated AI interface does not mean that the system performs actual analysis. It is important to distinguish between interface design, implementing an AI service, and validating its results.

---

## 🔮 Future Improvements

- Integrating an actual AI service to analyze compatibility while explaining the evaluation criteria and limitations.
- Adding an optional database to save and retrieve professional profiles across sessions.
- Expanding the collection of career opportunities while maintaining the reliability of requirement data.
- Improving recommendations to help prioritize skill development.

---


- **العرض التجريبي المباشر:** [https://dev-alignment-helper.lovable.app]
- **مستودع GitHub:**
     [https://github.com/mahaalzenati/dev-alignment-helper]


---

## 👩‍💻 Author

**[Maha Alzenati]**

[LinkedIn](https://www.linkedin.com/in/maha-alzenati-gamedev/) · [GitHub](https://github.com/mahaalzenati)
