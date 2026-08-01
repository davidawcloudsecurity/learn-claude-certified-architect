### Projects and Skills
Projects carry context
- What background knowledge and standing instructions apply to this workstream.

Skills define procedures
- How a specific task should be executed, consistently, every time.

| Component          | Think of it as                           | What it contains                                                                                                  |
| ------------------ | ---------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| **Project**        | **Workspace / Project Folder**           | Documents, uploaded files, previous conversations, knowledge base, persistent context.                            |
| **Skill**          | **Instructions / SOP / Prompt Template** | "Always respond this way", "Use this template", "Follow these rules". It's reusable guidance rather than data.    |
| **Artifact**       | **Finished Output**                      | A report, slide deck, email, document, meeting notes, or other deliverable.                                       |
| **Research**       | **Web Browser**                          | Searches the internet for information outside the model's knowledge.                                              |
| **Code Execution** | **Sandbox that runs code**               | Executes Python (and in some environments shell commands) to analyze data, transform files, generate charts, etc. |


### Use Cases
```
A business analyst produced a regulatory tracking report once a month. The task was consistent: take that month's regulatory updates, identify which applied to the portfolio, summarize the implications, and format the output per a defined template. The task was high stakes, but with a repeatable structure.

For the first two months, she ran the workflow in Chat. Each session, she uploaded the regulatory documents, re-pasted the portfolio context, and re-typed the format instructions. She ran a verification step on every numeric figure. She caught two errors in month one and one in month two, all before the report went out.

In month three, she rebuilt the workflow using the capability layer. The portfolio context and standing format instructions went into the Project, prior reports went into the knowledge base, she enabled a Skill for the report output format, and numeric calculations moved to Code Execution.

The time per session dropped from 65 minutes to 30, and the verification step still ran. No errors were found in months three through eight.
```
### What the analyst asked before rebuilding
- Which parts of this task are the same every time? |	Standing instructions + Skill
- Which reference material recurs across sessions? |	Knowledge base
- Which outputs need to be computed correctly, not just "sound right"? | Code Execution
- Which context do I want to carry across sessions without re-entry? | Memory

### Decision logic
Task profile | Model
- Routine, structured extraction or classification at volume | Haiku
- Most professional drafting, synthesis, and analysis | Sonnet
- Complex judgment, high-stakes output, ambiguous or multi-layered inputs |	Opus

### Pick the right feature for the job
Card	Configuration	Reason
| Card  | Configuration                              | Best For                                                 | Keywords                                        |
| ----- | ------------------------------------------ | -------------------------------------------------------- | ----------------------------------------------- |
| **A** | Project + Skill + Sonnet                   | Repeated work with the same structure                    | recurring, template, knowledge, consistency     |
| **B** | Research + Sonnet                          | Looking up current information                           | latest, recent, competitors, news               |
| **C** | Code Execution + Haiku/Sonnet              | Data analysis and calculations                           | CSV, Excel, math, statistics                    |
| **D** | Project (Knowledge Base) + Artifact + Opus | Large, complex analysis using many documents             | board reports, strategy, ambiguity              |
| **E** | Chat + Artifact + Sonnet                   | One-off writing                                          | email, letter, proposal                         |
| **F** | Project + Code Execution + Skill + Sonnet  | Recurring workflow involving calculations and formatting | monthly reports, dashboards, financial analysis |

| Scenario                                                                                 | Correct Card                                      | Reason                                                                                                                                   |
| ---------------------------------------------------------------------------------------- | ------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| **S1. Marketing director needs competitors' product launches in the last 90 days.**      | **B – Research + Sonnet**                         | Requires **current information** that is newer than the model's training data, so web research is needed.                                |
| **S2. Weekly meeting notes using the same template for six months.**                     | **A – Project + Skill + Sonnet**                  | A **recurring structured task** with a consistent format. The Project stores context, and the Skill ensures the same workflow each week. |
| **S3. Strategy consultant writes a 15-page board analysis from four reports.**           | **D – Project + Artifact + Opus**                 | Requires **deep reasoning**, interpretation of multiple documents, handling ambiguity, and producing a high-quality deliverable.         |
| **S4. HR analyst calculates response rates from 800 survey responses.**                  | **C – Code Execution + Haiku/Sonnet**             | Primarily a **data analysis task** involving calculations, percentages, and identifying departments below a threshold.                   |
| **S5. Monthly variance analysis comparing actuals to budget using a standard template.** | **F – Project + Code Execution + Skill + Sonnet** | A **recurring workflow** that combines calculations, standardized formatting, and reusable instructions.                                 |
| **S6. Procurement manager drafts a one-off reply to a vendor.**                          | **E – Chat + Artifact + Sonnet**                  | A **single drafting task** with no recurring workflow, research, or calculations required.                                               |

| Card  | Remember It As       | Think Of...                                              |
| ----- | -------------------- | -------------------------------------------------------- |
| **A** | **Always the same**  | Recurring templates and structured work                  |
| **B** | **Browse**           | Current events, latest news, web research                |
| **C** | **Calculate**        | Excel, CSVs, statistics, numeric analysis                |
| **D** | **Deep Think**       | Complex reports, strategy, multiple documents            |
| **E** | **Email/Edit**       | One-off writing or drafting                              |
| **F** | **Factory Workflow** | Repeated process with calculations and a standard output |

| Question                                                      | Why it matters                                                                                                                                         | Points you to                          |
| ------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------- |
| **Does it need the latest information?**                      | The AI's built-in knowledge may be outdated. It needs access to external sources to get fresh data.                                                    | **Research (Card B)**                  |
| **Does it involve calculations?**                             | Language models are good at reasoning but not always reliable at arithmetic or large-scale data processing. A code environment gives accurate results. | **Code Execution (Card C/F)**          |
| **Is it a recurring workflow?**                               | Repeated tasks benefit from saved context, files, and reusable instructions instead of starting from zero every time.                                  | **Project + Skill (Card A/F)**         |
| **Does it require deep reasoning across multiple documents?** | Large, ambiguous problems need stronger reasoning, document understanding, and synthesis.                                                              | **Project + Artifact + Opus (Card D)** |
| **Is it just a one-off drafting task?**                       | No memory, automation, or special tools are required. The AI just needs to create the content.                                                         | **Chat + Artifact (Card E)**           |

  
### Anatomy of an Effective Prompt
The component stack
| Component         | What it Controls                      | Why It Matters                                                                          | Example                                                                        |
| ----------------- | ------------------------------------- | --------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| **Role**          | Who Claude should act as for the task | Sets the vocabulary, expertise level, perspective, and assumptions                      | "Act as a financial analyst" / "Act as a security architect"                   |
| **Context**       | Background information Claude needs   | Provides details Claude cannot know: audience, situation, history, documents, decisions | "This is for a board presentation. The company is migrating workloads to AWS." |
| **Task**          | The specific action to perform        | Gives a clear objective. A strong prompt usually has one main action verb               | "Analyze the risks" / "Summarize the report" / "Compare these architectures"   |
| **Constraints**   | Boundaries and requirements           | Controls the output so it is usable without heavy editing                               | "Keep it under 500 words. Use a professional tone. Include pros and cons."     |
| **Output Format** | The structure of the answer           | Defines how the result should be presented                                              | "Create a table" / "Write a 3-paragraph memo" / "Generate a checklist"         |

### Weak prompt: everything left implicit
```
Weak prompt
"Write a summary of our quarterly operations."
### Strong prompt: components made explicit
```
### Task Decomposition for Complex Requests

| Concept                                        | Explanation                                                                                                            | Example                                                                                                                       |
| ---------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| **Task Decomposition**                         | Breaking a large, complex request into smaller, ordered steps that the AI can execute and verify one at a time.        | Instead of asking "Evaluate three vendors and recommend one", split it into criteria → scoring → trade-offs → recommendation. |
| **Why it matters**                             | A single large prompt forces the AI to perform multiple reasoning tasks at once, which can result in shallow analysis. | AI may invent criteria, score vendors, compare trade-offs, and recommend without showing the logic clearly.                   |
| **Single Prompt Approach (Weak)**              | One instruction containing multiple hidden tasks.                                                                      | "Evaluate these three vendors and tell me which one to pick."                                                                 |
| **Problem with Single Prompt**                 | The AI must decide the evaluation criteria, analyze data, compare options, and make a recommendation simultaneously.   | The recommendation may be difficult to audit or challenge.                                                                    |
| **Decomposed Approach (Better)**               | Separate the problem into logical stages where each stage produces an output that can be reviewed.                     | 1. Define criteria → 2. Score vendors → 3. Identify trade-offs → 4. Recommend                                                 |
| **Step 1: Derive Criteria**                    | Identify what factors matter before evaluating options.                                                                | "From the requirements document, define evaluation criteria and assign weights."                                              |
| **Step 2: Score Vendors**                      | Evaluate each option against the agreed criteria.                                                                      | "Score each vendor based on security, cost, reliability, and features."                                                       |
| **Step 3: Raise Trade-offs**                   | Identify where options differ and what compromises exist.                                                              | "Vendor A is cheaper but has fewer enterprise features."                                                                      |
| **Step 4: Recommend**                          | Make a final decision based on the previous analysis.                                                                  | "Recommend Vendor B because it scored highest against the weighted criteria."                                                 |
| **Intermediate Results**                       | Each step creates a checkpoint that can be reviewed before moving forward.                                             | If criteria are wrong in Step 1, fix them before scoring vendors.                                                             |
| **Auditability**                               | Decomposition makes the reasoning process easier to review and explain.                                                | Stakeholders can understand why a recommendation was made.                                                                    |
| **One Conversation vs Multiple Conversations** | Keep related sequential steps together so the AI remembers previous outputs.                                           | Criteria → scoring → trade-offs → recommendation should stay in one conversation.                                             |
| **When to Start a New Conversation**           | Move to a new chat when the task is independent or the conversation becomes too long and context quality drops.        | Vendor evaluation and writing a marketing email should be separate conversations.                                             |

Strong prompt
```
"You are an operations analyst (role). I am preparing a one-page update for our regional director, who cares about throughput and cost, not process detail (context and audience). Summarize the attached Q3 operations data (task), covering only the three metrics that moved more than 10 percent against target (constraint). Format as a short headline followed by three bullet points, each one sentence (output format)."
```
| Without Decomposition     | With Decomposition       |
| ------------------------- | ------------------------ |
| "Do everything"           | "Do one stage at a time" |
| Hard to verify            | Easy to review           |
| Hidden reasoning          | Visible checkpoints      |
| Higher chance of mistakes | Easier correction        |

### Decompose a Parallel Case
The key idea:
```
When multiple outputs depend on the same source of truth, do the common analysis first, then create the different deliverables.
```
| Concept                          | Explanation                                                                           | Example                                                              |
| -------------------------------- | ------------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| **Parallel Case Decomposition**  | Breaking one large request into multiple deliverables that share common information.  | One policy document → announcement + FAQ + executive briefing        |
| **The Problem**                  | If you create each output separately, each one may interpret the source differently.  | Announcement says one thing, FAQ says another                        |
| **Shared Foundation**            | Extract the important facts once and use them as the source of truth for all outputs. | Policy changes and their practical impact                            |
| **Step 1: Extract Information**  | First identify the key facts before writing anything.                                 | "Extract all policy changes and explain their business impact."      |
| **Step 2: Validate Extraction**  | Confirm the extracted information is accurate before using it.                        | "Review the extracted changes against the original policy document." |
| **Step 3: Create Deliverable 1** | Use the validated foundation to create the first output.                              | Staff announcement                                                   |
| **Step 4: Create Deliverable 2** | Reuse the same foundation but change the audience and purpose.                        | FAQ for employees                                                    |
| **Step 5: Create Deliverable 3** | Compress the same information for another audience.                                   | Executive briefing                                                   |
