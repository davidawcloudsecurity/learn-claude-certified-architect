### Projects and Skills
Projects carry context
- What background knowledge and standing instructions apply to this workstream.

Skills define procedures
- How a specific task should be executed, consistently, every time.

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
- Project + Skill · Sonnet	Recurring structured task, stable context, fixed output format
- Research · Sonnet	Current-information task; window post-dates reliable training-data recall
- Code Execution · Haiku or Sonnet	Calculation on a defined dataset; result must be accurate
- Project (knowledge base) + Artifact · Opus	Nuanced multi-source analysis, ambiguous inputs, high-stakes deliverable
- Chat + Artifact · Sonnet	One-off drafting task; no capability layer needed
- Project + Code Execution + Skill · Sonnet	Recurring workflow with verified numeric outputs and consistent format
