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
What the analyst asked before rebuilding

Question|	Layer it pointed to|
Which parts of this task are the same every time?|	Standing instructions + Skill|
Which reference material recurs across sessions?|	Knowledge base|
Which outputs need to be computed correctly, not just "sound right"?|	Code Execution|
Which context do I want to carry across sessions without re-entry?|	Memory|
