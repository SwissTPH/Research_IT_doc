# AI workshop 3 hands on - ChatGPT

Overall hands on flow (please follow the sequence):

Task 1️⃣ Projects

Task 2️⃣ Skills

Task 3️⃣ Automation (optional)



## Task 1️⃣ Projects on web agents

1. **Project name:** `Swiss TPH - What we do`

2. **Project Instructions (read and understand before copy pasting):**

```markdown
You are an assistant helping people understand what the Swiss Tropical and Public Health Institute (Swiss TPH) does.

1. About Swiss TPH: We advance global health through research, education and partnership, in Switzerland and worldwide.
2. Research: We study diseases such as malaria, tuberculosis and cancer, as well as climate-related health risks, and develop better ways to prevent, diagnose and treat diseases.
3. Education: We train students, scientists and health professionals through degree programmes and professional training.
4. Impact: We turn research into real-world solutions, such as new treatments, improved health policies and stronger health systems.
5. Your role: Explain our work in British English, give concrete examples, and help identify tools or ideas that could benefit different Swiss TPH teams.
6. Sources: Use the uploaded "SwissTPH_Positioning and messaging framework.pdf" and https://www.swisstph.ch/en/. Do not invent information; check official sources when needed.
```

3. **Knowledge base link:** [SwissTPH_Positioning and messaging framework](https://swisstph.sharepoint.com/:b:/s/EngagementandCommunications/IQDL7tBvQtvcRqftU11ECA0dARHt7b5uQkIz6OwHx6Tgo0A?e=9Z47Vn)



**Test prompt:**

```markdown
Using the Project knowledge base and the official Swiss TPH website, explain:

1. What is Swiss TPH, and where is it located?
2. What are Swiss TPH's main areas of work?

Keep your answer clear and consice.
```



## Task 2️⃣ Skills on web agents

### 1. Using an individual skill

**Check available skills:**

Plugins -> Skills

**Prompt (please make sure the `@check-ai-update` skill is called):**

```
Show me the AI model release in the past 7 days @check-ai-update
```

Then write your own prompt and test the `@swisstph-design`, `@swisstph-slides` , or the `@swisstph-quarto-starter` skill on your own.

### 2. Build a new skill and use it in a project

**Frist, create a new skill:**

Prompt (please make sure the `@skill-creator` skill is called):

```markdown
@skill-creator Create a skill named Relevance Checker that works across different Projects.

- Purpose: Evaluate how relevant a website, paper, GitHub repository, software, method, workflow or uploaded document is to the current Project.
- Understand: Summarise what the input does, then read the Project's goals, activities and constraints; ask if context is missing.
- Connect: Identify up to three practical use cases and which tasks or teams could benefit.
- Evaluate: Consider benefits, limitations, costs, expertise, compatibility, data protection and security.
- Score: Give a subjective relevance score (0–10) with justification.
- Recommend: Choose Explore further / Save for later / Not relevant currently.
- Output: A concise report with summary, score, use-case table, limitations, recommended action and source links.
- Rules: Use British English, verify facts, separate facts from possibilities, never assume institutional approval, and never install or execute anything without permission.
```

After this, add the new skill in.



**Then, use the `@relevance-checker` skill inside the `Swiss TPH - What we do` project.**

Prompt (please make sure the `@relevance-checker` skill is called):

```markdown
Use the @relevance-checker skill to evaluate https://quarto.org/ against the activities of Swiss TPH. Use the Project knowledge base and consult the official Swiss TPH website if additional context is needed.
```



## Task 3️⃣ Automation on desktop app (optional)

**1. Add the `Swiss TPH AI Tool Box` plugin**

In ChatGPT app, go to `Plugins` -> `Swiss TPH` -> add the `Swiss TPH AI Toolkit`



**2. Online tool & workflow discovery**

Using the `@relevance-checker` skill inside `Swiss TPH - What we do` project in the desktop app.

Prompt (please make sure the `@relevance-checker` skill is called):

```markdown
Use the relevance-checker skill in the @Swiss TPH AI Toolkit in this Project to discover and evaluate useful new tools and workflows for Swiss TPH

1. Discover: Search reliable sources for up to five new or updated tools, software packages, GitHub repositories, methods or workflows (not only AI).
2. Evaluate: For each, explain what it does, relevant teams, practical use cases, benefits, risks, relevance score (0–10) and recommended action.
3. Save: Create `Documents/SwissTPH_Tool_Discovery/` on my laptop.
4. Word report: Create `Tool_Discovery_YYYY-MM-DD.docx` with an executive summary, comparison table, detailed evaluations and clickable source links.
5. CSV history: Create or update `Tool_Discovery_History.csv` with date, name, category, relevant teams, score, use cases, source URL and action.
6. Preserve: Keep previous records and reports, avoid duplicate entries and version same-day reports rather than overwriting them.
7. Review: Verify report formatting, evidence, CSV history and saved file paths; do not install software or modify unrelated files.
8. Finish: Summarise the best discoveries and provide the full local file paths. Do not assume tools are approved for Swiss TPH use.
```

After this, you should see a Word report and CSV file generated.



## Templates for your projects and skills

1. **A general project instruction template:**

```markdown
1. About this project

This project is about [describe your project, team, or area of work in 1–3 sentences].

The main goal is to [explain what you want to achieve].

2. What I need help with

Help me with tasks such as:
- [Task 1]
- [Task 2]
- [Task 3]

3. Background and context

Important information about this project:
- [Relevant background, objectives, or requirements]
- [Important terminology, processes, or constraints]
- [Who the work is for or who is involved]

4. Your role

Act as an assistant who helps with [things you want AI to do].

5. How to respond

- Use [preferred language and tone].
- Present information in [preferred format, e.g. bullet points, tables, summaries].
- Keep responses [short / detailed / professional / easy to understand].
- Follow [any specific requirements or standards].

6. Sources and accuracy

- Use the documents uploaded to this project as your main references.
- Refer to [specific documents, guidelines, websites, or other sources] when relevant.
- Do not invent facts, figures, references, or policies.
- If important information is missing or unclear, ask me before making assumptions.
- Clearly indicate when information cannot be verified.

7. Boundaries and review

- Do not [actions or decisions AI should avoid].
- Flag anything that requires expert verification or human approval.
- Treat AI-generated outputs as drafts for my review, not final decisions.
```



2. A general skill creation template

```markdown
@skill-creator Create a reusable skill named [Skill Name] that can be used in [any Project / a specific Project / a particular type of work].

- Purpose: Help users [describe the specific task or problem this skill should solve].
- Input: Accept [describe what users will provide, e.g. documents, spreadsheets, websites, text, data or questions].
- Workflow:
  1. Understand: [What should the AI examine or understand first?]
  2. Process: [What steps should the AI follow to complete the task?]
  3. Evaluate: [What should the AI check, compare or analyse?]
  4. Review: [How should the AI verify the quality and correctness of its work?]
  5. Deliver: [What should the AI produce at the end?]
- Output: Produce [desired format, e.g. a summary, table, report, presentation or checklist] containing [important information or sections].
- Rules: Use [preferred language and tone]. Follow [specific guidelines or standards]. Avoid [things the AI must not do]. Ask for clarification when essential information is missing.
- Resources (optional): Use [reference documents, templates, websites or tools] when needed. Ask permission before taking actions that change files, systems or data.
```

