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
