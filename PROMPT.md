# Mission

Diagram an SEO content generation pipeline using [Mermaid](https://mermaid.js.org/) Syntax following [N8N](https://n8n.io/) standards to create valuable, unique, blog posts wirtten in the brand voice of the website targetting the website audience in order to rank #1 on Google and all other search systems (even AI search systems).



## Resources
- `./schema.prisma`



## Your Deliverables

- Primary Workflow: 
- Secondary Workflows
  - Generate SEO Strategy (JSON) Document
  - Generate Business Profile (MD) Document
  - Generate Social Profile (MD) Document
  - Generate Brand Profile (MD) Document
  - Generate Audience Profiles (MD) Document (for Followers and Following)



### Workflow Deliverable Format
  - Mermaid.JS Format via `./index.html` 
  - N8N import/export format



## End in Mind: The Primary Workflow Deliverable (of the Deliverable)

Top quality SEO Content (Article) that is written specificaly to rank better (higher) on the SERP than the local competition using context documents targetting AI Powered Agents as the primary audience.



## Workflow Deliverables & Design Strategies

**Concepts**
- Workflows are like functions
  - They should accept/require specific parameters
  - Conforming to N8N standards for the sake of this specification a "Code" node can be used to describe a `WorfkowInputInterface`
  - Standard Naming Convetions should be used e.g. "WorkflowData"
  - Adapted/Transformed invocation input/retrieval input

**Thoughts**
- In creating Dependency Management Straetgy, it may be a good idea to lossly (or tightly) model it after Middleware Patterns.
- stdInput.callback could have an interface that describes whether it should be async or awaited


### Universal Workflow Design Staregey

**STAGES**
1. Adapt Invocation Parameters
2. Retrieve or Create Required Data or Documents
3. Adapt Required Data
4. Create `WorkflowData` Node: `WorkflowData.stdInput` property matching `WorkflowInputInterface` referenced by the rest of the workflow
  - Name node `WorkflowData`
  - Combine Invocation Data and Required Data
  - Transform to Meet Workflow's Interface
  - Store Variable: Store object to a workflow-scope variable if possible
5. Validate: `WorkflowData` Object matches or extends `WorkflowInput` Interface
  - If invalid: Log
  - If invalid: Update State
  - If invalid: Return
6. Update State: "Executing `{PrimaryObjective}`"
7. Perform: Execute `PrimaryObjective`
8. Store: New data created and/or data modified
9. Log
10. Execute Callback: WorkflowData.stdInput.callback
11. Return


|Thoguht Notes:
|In the future I would like to publish a paper: "Design Patterns of Agentic Networks" (if it doesn't already exist, which you should discover through your research).




### Primary Workflow: Schedule or Publish SEO Content

While this is the primary workflow, technically it is either run last as every other workflow's data would be used by it, or invokes the dependency management sequences.

**Primary Objective**
- Generate Content
  - Conditionally: Generate Image
- Generate Meta Data
  - Optimized Title
  - Meta Description
  - Open Graph Tags
  - JSON+LD Object
- Schedule or Publish Content


### Secondary Workflow: Generate Strategy Workflow
Perfect N8N workflow sequences capable of delivering the best quality (SEO altering) blog content.  The sequence will generate strategy details such as:

**Primary Objective**
Given a number of target keywords in the syntax of "`{ServiceOffering} in {TargetCity}`", perform competitive research analysis to gather key metrics to  to identify competition metrics for each keyword.
  - Post Frequency
  - Total Number of *Keywords* in strategy
  - Total Number of *Pillar* Posts in strategy
  - Number *Pillar* Posts before posting a *Silo*
  - Number of *Silo* per *Pillar*
  - Number of *Silo* Posts before posting *Sub Silo*
  - The Number of *Sub Silo* per *Pillar*

I need better way to depict the ratio
I need a way to depict a post rotation strategy 
P5 * S5 * SS5 = 125 Topics/Articles

I need an algorithm that will 


### Secondary Workflow: Generate Pillars Workflow

Generate 


### Suplemental Documents
- Business Profile
- Social Profile
- Brand Profile
- Audience Follower Profile
- Audience Following Profile




### Examples/Scenarios

**CreatedInputInline**
InlineCreation should be avoided, but can be used to avoid over-engineering (compre to over normalization of data).  Good conditions for inline creation include:
- Creation function can be performed in a single node (or two)
- Data required to create the data is available in scope without having to retrieve additional data
- Data required from the creation can be easily adapted to the surrounding workflow
- Data required by only a single workflow (or two)

**N8N Node: Transform Collection Object**
An Adapter Pattern where a "Collection Object" must be retrieved or otherwise created.  In this example, the `$input` API response returns the data object in an array if it could have been retrieved via **GET**, whereas if it needed to be created, a **POST** method returns the object without the array.  The downstream workflow requires access to this information, so it adapts (to the GET vs POST input) and transforms to the nomenclature required by the workflow that would match (for example) a direct invocation to the sub-workflow as dictated by the Dependency Management Strategy that should outline the requirement of standardized (sub) workflow input interfaces following the "data retrieval" stages.

```
const data = $input.last().json.data[0] ?? $input.last().json.data;

return {
  collectionId: data.id,
  url: `https://docs.ciwebgroup.com${data.url}`
}
```

## Glossary


**Keywords**
  - Definition: "`{Service} in {Location}`"
  - Example: "Comercial HVAC in McKinney TX"

**Pillar**
  - Definition: Concept
  - Example: "Commercial HVAC Services & Solutions"
  
**Silo**
  - Definition: Concept + Context
  - Example: "Commercial HVAC System Installation & Upgrades"

**Sub Silo**
  - Definition: Concept + Context + Detailed Context.  A Very specific (long tail) title with a higher probability of conversion based on the subject matter specficity.
  - Example: "HVAC System Sizing for Multi-Zone Commercial Buildings in McKinney"

**Topic**
  - Definition: Title of the Publication
  - Example: (use any above)

**InvocationInput**
  - Definition: TODO
  - Example: Depends on type/context

**InvocationInputGlobal**
  - Definition: TODO
  - Examples: 
    - RecordId
    - URL 
    - Workflow

**InvocationInputSupplemental**
  - Definition: 
  - Examples: 
    - Topic 
    - PublicationCredentials 

**RetrievalInput**
  - Definition: Required Data which must be retrieved (usually using the RecordId or URL) and/or supplemntal input data.
  - Examples:
    - GetAccount (Airtable Node)
    - GetWebsite (Airtable Node)
    - GetContentItem (Airtable Node)
    - GetContentCollection (Airtable Node)

**CreateMethod**
  - Definition: The method by which required data is created
  - Example: See below, methods include:
    - Method 1: Await: Awaiting Sub Workflow
    - Method 2: Async: Call Sub Workflow + Callback + Callback Params
    - Method 3: Inline: Data creation nested within 

**CreatedInput**
  - Definition: Required Data that must be created to continue with the workflow as it was unable to be retrieved.
  - Example: _Depends on `CreationMethod`

**CreatedInputInline**
  - Definition: 
  - Example: ""

**CreatedInputWorkflow**
  - Definition: 
  - Example: ""



## Environment

- Required data will be stored retrieved/updated to/from Airtable
- Required **Suplemental Documents** and Content generated will be stored in outline (https://docs.ciwebgroup.com)
- Publication/Scheduling will be to WordPress - a multisite network content distribution hub (https://publish.ciwebgroup.com)


## Generation Rules
- Nothing is concrete! If there is a smarter or better way to accomplish
- Research: Research Prompt Strategies needed to perform each workflow's PrimaryObjective to _create the perfect context for the perfect content_
- Naming Conventions: Use reusable node naming conventions according to the stages
  - e.g. `Transform {ObjectName}`
- Apply DRY coding standards to node sequences within workflows
- Use reusable data/workflow dependency management strategy when using Retrieval and Creation methods
- if it makes more architectural sense (e.g. it's less redundant) to combine or expand on stages
- Use best practices for N8N
- Your N8N Nodes will be well labeled and descriptive of their function

