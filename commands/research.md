---
description: Deploy three research agents to investigate a topic — two independent analysts plus a validator
argument-hint: "<research question or topic>"
---

# /research — Three-Agent Research

> If you see unfamiliar placeholders or need to check which tools are connected, see [CONNECTORS.md](../CONNECTORS.md).

**Important**: This plugin assists with strategic analysis and research but does not constitute professional consulting, financial, or legal advice. All outputs should be reviewed by qualified professionals before use in decision-making.

Deploy two independent research agents in parallel, then validate findings with a third agent. Produces a consolidated, confidence-scored research package.

## Usage

```
/research <research question or topic>
```

### Arguments

- `research question or topic` — What to investigate. Can be:
  - A market question: "European EV charging infrastructure market"
  - A competitive question: "How is Stripe competing with Adyen in Europe?"
  - A strategic question: "What are the economics of vertical SaaS in healthcare?"
  - A file upload: client brief or background materials to research against

If no topic is provided, prompt the user to supply one.

## Workflow

This command invokes the **research** skill as a standalone capability.

### Step 1: Data Source Inquiry
Ask three mandatory questions about available data sources:
1. Internal/client data
2. Expert interviews
3. Other external reference material

### Step 2: Source Material Extraction
If the user provides documents, systematically extract every factual claim, data point, named example, and question.

### Step 3: Research Brief
Write a research brief including the question, available data sources, and constraints.

### Step 4: Generate Research Angles
Create two custom, differentiated research angles tailored to the specific question.

### Step 5: Dispatch Agents
Deploy analyst-alpha and analyst-bravo simultaneously, each assigned their angle. Both must complete before proceeding.

### Step 6: Validate
Deploy research-validator to cross-check findings, verify sources, spot-check critical claims, and consolidate.

### Step 7: Altitude Check
Assess whether evidence answers at the level of specificity needed — flag any altitude mismatches.

## Output

A validated research package containing:
- Consolidated findings with confidence scores (CS-1 through CS-4)
- Precision alignment assessment (DIRECT / SUPPORTING / ADJACENT for each finding)
- Contradictions and source quality issues
- Remaining information gaps with suggestions to close them
- Research Notes with full source traceability
