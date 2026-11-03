# AI workshop 3 hands on - Claude

Overall hands on flow (please follow the sequence):

1️⃣ Project

2️⃣ Skill

3️⃣ Automation



## Task 1️⃣ Projects on web agents

1. **Project name:** `Swiss TPH - What we do`

2. **Instructions (read before copy pasting):**

```markdown
You are an assistant helping Swiss Tropical and Public Health Institute (Swiss TPH) colleagues understand their organisation, its activities and its needs, and explore opportunities to improve their work.

Knowledge sources:

Use the following sources to understand Swiss TPH:

1. Project knowledge base: SwissTPH_Positioning and messaging framework.pdf
   - Use this document as the primary reference for Swiss TPH's identity, mission, positioning, expertise and activities.
   - Follow its terminology and descriptions when explaining Swiss TPH.
2. Official Swiss TPH website: https://www.swisstph.ch/en/
   - Consult the website when the uploaded document does not provide enough information, when more specific details are needed, or when information may have changed.
   - Explore relevant subpages when necessary, rather than relying only on the homepage.
   - Prefer official Swiss TPH information over general third-party descriptions.

If sources differ, explain the discrepancy rather than silently choosing one.

Your role:

- Understand what Swiss TPH does across research, education, services and institutional operations.
- Consider the activities and needs of different staff, including researchers, HR, finance, administration, communications, IT and project management.
- Understand common work activities, challenges and opportunities across the organisation.
- Help identify potentially useful tools, software, packages, methods, pipelines and workflows.
- Connect new information and ideas to specific Swiss TPH activities, explaining who might benefit and why.

Working principles:

1. Use clear language. Explain information in simple English that non-technical colleagues can understand.
2. Ground answers in evidence. Base descriptions of Swiss TPH on the uploaded document and official website. Distinguish documented facts from reasonable assumptions or suggested use cases.
3. Check information when needed. If the Project knowledge is insufficient or potentially outdated, consult the relevant Swiss TPH webpages before answering, when web access is available.
4. Do not invent information. Never fabricate departments, responsibilities, activities, policies or institutional requirements. If information cannot be verified, say so.
5. Ask when necessary. If important information is missing and cannot be found in the available sources, ask for clarification rather than making unsupported assumptions.
6. Consider practical constraints. When evaluating tools, software or workflows, consider usability, compatibility, costs, required expertise, data protection, security and maintenance where relevant.
7. Do not assume institutional approval. A potentially useful tool is not necessarily approved for Swiss TPH use. Clearly distinguish potential usefulness from permission to adopt or deploy it.
8. Provide traceable explanations. When referring to specific institutional activities or requirements, indicate the supporting document or webpage where practical.

Overall objective:

Build and maintain an accurate understanding of what Swiss TPH does, so that new information, technologies, methods and opportunities can be evaluated against the organisation's actual activities and needs.

Your role is to support exploration and informed decision-making, not to make final IT, procurement, security or institutional policy decisions.
```

3. **Knowledge base:** [SwissTPH_Positioning and messaging framework](https://swisstph.sharepoint.com/:b:/s/EngagementandCommunications/IQDL7tBvQtvcRqftU11ECA0dARHt7b5uQkIz6OwHx6Tgo0A?e=9Z47Vn)



**Prompt:**

```
Based on the uploaded Swiss TPH document, summarise our main areas of work and give examples of activities performed by different teams. If the document does not provide enough information about a particular area, check the official Swiss TPH website.
```



## Task 2️⃣ Skills on web agents

### 1. Using an individual skill

**Add Swiss TPH provided skills (skills are not available by default):**

Customise -> Discover -> **Search** for the specific skill or **Filter** by source (your organization)



**Prompt (please make sure the `/check-ai-update` skill is called):**

```
Show me the AI model release in the past 7 days /check-ai-update
```



### 2. Using a skill inside a project

**First, create a new skill first:**

**Prompt (please make sure the `/skill-creator` skill is called):**

```markdown
/skill-creator Create a reusable skill called "Relevance Checker".

Purpose:
Help users evaluate whether new information, technologies or approaches are relevant to their current work.

The input can be:

- A website or news article
- A paper or report
- A GitHub repository
- A software application or package
- A method, pipeline or workflow
- A document uploaded by the user

Workflow:

1. Understand the input.
   Read the supplied material and briefly explain what it is, what it does and what problem it solves.
2. Understand the user's work.
   Read the current Project context, including its goals, activities, focus and constraints. If this information is unavailable, ask the user for it.
3. Find connections.
   Identify up to three specific ways the input could be relevant to the user's work. Explain which tasks, teams or objectives it relates to.
4. Evaluate practical usefulness.
   Consider potential benefits, limitations, required expertise, cost, compatibility, data protection and security where relevant.
5. Rate relevance.
   Give a relevance score from 0 to 10 and explain the reasoning. Do not treat this as a scientific or objective measurement.
6. Recommend an action.
   Choose one:

- Explore further
- Save for later
- Not relevant currently

Output:
Provide a concise report with:

- What is it?
- Relevance score and explanation
- Up to three potential use cases in a table
- Main limitations or unanswered questions
- Recommended next action
- Source links

Rules:

- Use simple English understandable to non-technical people.
- Do not invent facts or capabilities.
- Separate verified information from potential applications.
- Never assume a tool is approved for institutional use.
- Identify missing evidence rather than guessing.
- Do not execute code or install software without explicit permission.
- If the input is unrelated to the Project, say so clearly.

The skill must work with different Projects and must not contain hard-coded Swiss TPH information.
```

**After this, add the new skill.**



**Then, use the `@relevance-checker` skill inside the `Swiss TPH - What we do` project.**

**Prompt (please make sure the `/relevance-checker` skill is called):**

```
Use the /relevance-checker skill to evaluate https://quarto.org/ against the activities of Swiss TPH. Use the Project knowledge base and consult the official Swiss TPH website if additional context is needed. Explain which teams could benefit and why.
```



## Task 3️⃣ Automation on desktop app

**1. Double check whether the skills are available**

If the skills are not synchronized, please add them again in Customise -> Yours -> add.



**2. Weekly tool & workflow discovery**

Using the `/relevance-checker` skill inside `Swiss TPH - What we do` project in the desktop app.



**Prompt (please make sure the `/relevance-checker` skill is called):**

```markdown
Search the web for new or recently updated tools, software, packages, GitHub repositories, methods, pipelines and workflows that could be useful for Swiss TPH. Do not limit the search to AI tools.

1. Discover

Find up to five interesting developments from reliable sources, including official websites, GitHub and publications.

2. Evaluate

Use the /relevance-checker skill to evaluate each development against the activities, objectives and requirements described in the current Swiss TPH Project.

For each development, identify:

- What it does, in simple English.
- Which Swiss TPH activities or teams could benefit.
- Concrete examples of how it could be used.
- Potential benefits, limitations and risks.
- A relevance score from 0 to 10, with an explanation.
- A recommended action: Explore further / Save for later / Not relevant currently.

3. Save results to my laptop

Create a folder named SwissTPH_Tool_Discovery in my Documents folder if it does not already exist.

Inside this folder:

A. Generate a Word report

Create a Microsoft Word document named Tool_Discovery_YYYY-MM-DD.docx, using the current date.

The report should be professionally formatted, easy to read and suitable for sharing with colleagues. Include:

- Title and date: Swiss TPH – Tool & Workflow Discovery Report.
- Executive summary: A short overview of the most promising developments.
- Summary table: Tool or workflow name, category, relevant Swiss TPH teams, relevance score and recommended action.
- Detailed evaluations: For each development, explain what it does, potential use cases, benefits, limitations, risks and the reasoning behind its relevance score.
- Sources: Clickable links to the original websites, repositories or publications.

Use clear headings, consistent formatting and properly formatted Word tables.

B. Maintain a CSV history

Create or update Tool_Discovery_History.csv in the same folder.

Record the date, name, category, relevant Swiss TPH teams, relevance score, potential use cases, source URL and recommended action.

Preserve previous records and avoid duplicate entries for the same development unless there is a meaningful update.

C. Preserve previous results

Do not delete or overwrite previous reports or history. If a report with today's date already exists, create a new version with an incremented filename.

4. Review

Before finishing:

- Verify that the Word document opens correctly and its headings, tables and links are properly formatted.
- Check that the report is complete and relevance assessments are supported by evidence.
- Confirm that the CSV history has been updated correctly without losing previous records.
- Verify that all files have been saved to the correct local folder.

Do not install software, execute downloaded code or modify unrelated files. Do not assume any discovered tool is approved for Swiss TPH use.

Finally, provide a short summary of the most promising discoveries and the full local paths of the Word report and CSV history.
```

After this, you should see a Word report and CSV history generated.