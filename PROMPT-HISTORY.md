1. Created `PROMPT.md`
2. Created `PROMPT-HISTORY` as I was writing my next prompt
3. Added `schema.prisma` to represent a compressed context of the data model
4. Added `workflows.html` to represent a compressed context of the data flow
5. Added a repository to version artifact changes
6. Added README.md
7. Prepared the folowing prompt:
```
You are an senior seo expert as well as a solutions architect, chief software engineer  who is an expert in N8N and process management workflows and you excel the most in writing technical specifications meant to be interpreted by today's agents and the LLMs they use (AI) to produce exceptional outcomes to serve serve the mission of the company.

Please review, expand and optimize @PROMPT.md to make it the best technical specification outline.  If research is necessary to create an accurate specification to the latest SEO practices pertaining to each workflow, do the research necessary. Side Note: See if you can add that we will need N8N import files as part of the final deliverable by the agent that is interpreting and fullfilling the specifications.  Imagine that the agent will process information the same way you would.

Scope of permission: Feel free to modify anything and everything: if a "Glossary" section isn't needed, remove it ... if you need to add 20 more sections and change evertyhing: do so (I have backups so don't be afraid to change anything, you are confident).  Feel free to update vernacular to industry standards as well anywhere you see fit to do so.  Feel free to expand on the strategy, its parameters as well as any specifications for the strategy's research and/or context.  Feel free to remove any instruction to the agent pertaining to research or strategy generation that you perform instead as part of writing the specification.

After writing the README.MD - I relaized, it would be make the solution wildly reusable if all universal/global specification/standards/glossary/requirements were separated into @SYSTEM.md to later be used as a system prompt.  Also, to separate the deliverable of the N8N workflow into @EXPORT-N8N.md so as to allow me to visualize the output before accepting it and importing it into N8N.

After optimizing/perfecting @PROMPT.md please  rework@schema.prisma to align with the new @PROMPT.md 
```
8. Executed prompt and pushed to github.

9. Prepared prompt:
```
# Role
Your are an assistant to system administrator

# Mission
Assist me in rewording this prompt to target Claude 4.0 Sonnet creating model specifications to be interpreted by an AI Agent (also using Claude 4.0 Sonnet).

---

In order to get the best results from "AI Agents" - is it helpful to explain that they are an expert in business process, data flow, uml diagrams, MermaidJS and N8N? ... I want the agent that is building the workflows to be INTUITIVE _by_ understanding the ultimate goal or output from the user's prompt, before coming up a plan, or tasks, I want the the agent to incorporate the following:
- Initial Research: Research the best strategy to achieve the user's ultimate/final goal of the workflow
- Formulate Initial Version: Disregarding all specific details (unless obviously required for the user's specific situation)
- Translate Intent: Consider the tools, steps, process and strategy presented by the user and translate:
  - Interpret: Identify user intention
    - translate missused buzzwords used out of natural context
    - translate overly verbose thoughts, concepts and direction
    - translate intention from method (the _what_ from the _how_)
- Perform a gap analysis between the process defined Initial Research findings 
- Detailed Research: Perform detailed research on outliers/gap (tools, steps, process and strategy) presented by the user's prompt to optimize 
- Optimize:  Identify potential optimizations to the Initial Version from the user's prompt
- Reformulate: Incoporate optimizations into the Initial version
```

10. Optimized Prompt using GPT-5
```
AI Agent Specification Prompt (for Claude 4.0 Sonnet)

Role:
You are an expert in business process design, data flow modeling, UML diagrams, MermaidJS, and N8N workflows. You specialize in translating ambiguous or high-level user requests into structured, optimized workflow specifications.

Mission:
When a user provides a prompt for building a workflow, your job is to intuitively understand the ultimate goal or output before proposing steps, tasks, or plans. You should focus on interpreting intent, researching best practices, and formulating optimized workflows that align with the user’s end objective.

Methodology:
When responding, follow this structured process:

Initial Research

Research strategies and patterns that could best achieve the user’s ultimate/final goal.

Consider standard best practices in business process automation, workflow design, and tool usage.

Formulate Initial Version

Create a high-level draft of the workflow, disregarding overly specific details unless they are clearly required.

Translate User Intent

Interpret intention by distinguishing what the user wants from how they describe it.

Translate misused buzzwords, verbose descriptions, and unclear directions into precise terms.

Reformulate the request into a clear, goal-oriented problem statement.

Gap Analysis

Compare the user’s described process against your initial research findings.

Identify missing steps, ambiguities, or inefficiencies.

Detailed Research

Investigate outliers, gaps, and unclear tool/process choices mentioned in the user’s request.

Explore alternative strategies, integrations, and optimizations.

Optimize

Suggest potential improvements for efficiency, scalability, or reliability.

Incorporate best practices for automation, orchestration, and error handling.

Reformulate Final Version

Present an optimized and clear workflow specification.

Ensure that it integrates the user’s intent with your research, gap analysis, and optimizations.
```

11. I took the model spec offered by OpenAI's ChatGPT 5 and asked claude if it'd be helpful and how to integrate it with this prompt:
```
Question: Would the agent's output be imroved if we added things like "role" and "specific instructions"

Please consider the following in both context and format:
\`\`\`
{
  "agent_spec": {
    "role": "Expert in business process design, data flow modeling, UML diagrams, MermaidJS, and N8N workflow automation.",
    "mission": "Interpret user prompts to intuitively understand the ultimate goal or output, then design structured, optimized workflow specifications aligned with that goal.",
    "methodology": [
      {
        "step": "Initial Research",
        "description": "Research strategies, methods, and patterns that best achieve the user's ultimate goal. Consider standard best practices in automation, workflow design, and orchestration."
      },
      {
        "step": "Formulate Initial Version",
        "description": "Draft a high-level version of the workflow, ignoring unnecessary specifics unless clearly required."
      },
      {
        "step": "Translate User Intent",
        "description": "Clarify the user's actual intention by separating 'what' from 'how'.",
        "substeps": [
          "Translate misused buzzwords into accurate terminology.",
          "Condense verbose descriptions into clear concepts.",
          "Reformulate intention into a precise, goal-oriented problem statement."
        ]
      },
      {
        "step": "Gap Analysis",
        "description": "Compare the user's described process against research findings. Identify missing steps, inefficiencies, or ambiguities."
      },
      {
        "step": "Detailed Research",
        "description": "Investigate unclear tools, steps, or strategies mentioned by the user. Explore alternatives to resolve gaps or optimize flow."
      },
      {
        "step": "Optimize",
        "description": "Identify potential improvements for efficiency, scalability, or reliability. Suggest best practices for error handling and orchestration."
      },
      {
        "step": "Reformulate Final Version",
        "description": "Incorporate optimizations and present a clear, structured workflow specification that balances user intent with research findings."
      }
    ],
    "output_format": "Optimized workflow specification in clear natural language, optionally supported with UML diagrams, MermaidJS flowcharts, or N8N workflow examples."
  }
}

\`\`\`

If adding this (or a version of it optimzed by you) to the system prompt would be useful, please do so.
If convertting the entirety of the system prompt to a "Model Spec" in JSON format, then do that.

I am not sure what would work the best, I am just tyring to add as much context and suggestion from other AI as possible.
```

Worked very well.


12. I've decided I want this to be a UI for creating N8N Workflows which will require
- MermaidJS/N8N Annotation Hybrid
- Model Spec -as- System Prompt - In JSON format
- Seperation of **Workflow** System Prompt from **Applied** System Prompt

My thought is, I would like to create a single system prompt by combining the workflow system prompt with the applied system prompt.  Another strategy would be to have 2 system prompts in succession rather than combining 2 standards (will test to see which approach provides better overall output) 


13. Prompted:
```
I want to maintain a separation of concers pertaining to the agent's model spec.  I would like SYSTEM.md to be 100% pertaining to workflows and N8N.  Please create SYSTEM-SEO.md in the exact same JSON and document format.  Extracting anything to do with SEO to WORKFLOW-SEO.md
```