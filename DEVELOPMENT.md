# Development notes

---

Ultimate aim: Determine priority of patients: Low priority can get immediate outpatient treatment, high priority gets inpatient treatment

Find new/emerging biomarkers that wouldn't normally be considered, but could help with diagnosis. And explain why.

Emulate real life team in hospital for triaging with multiple agents

There are two systems (crews) in TriAgent:

1. Data analysis agent to mine patient data and identify most relevant biomarkers for triaging
2. Deep research agent for finding causal link. If not found, flag as potential research area

Refinement: Look at this patient's individual case with existing biomarkers and conditions, and then identify most relevant biomarkers to indicate diagnosis

- Aim to make the below pipeline cyclical and alllow constant querying and improving given new biomarker readings

## Scoping agent

- Refine user's initial research query
- Engage in clarification dialogues to get relevant information
- Provide symptoms and basic surface-level triage (basic check-up)
- Generate patient brief $B_1$ to feed to deep research crew

## Data Analysis Agent

- Take input from scoping agent to restrict database slightly
- Identify most relevant features to diagnosis and priority (ground truth from data) using vanilla ML and statistical methods
- Generate brief $B_2$ for remaining biomarkers to check sorted by relevance/importance.

## Research Supervisor Crew

- Inputs
    1. Patient brief of symptoms, descripton
    2. Statistical analysis of biomarkers and respective weights

- Main superviser formulates topic plan $T_p$, queries $q_i$ for each biomarker $x_i$
- Generate each $q_i$ using a LLM
- Each agent performs multi-source searches across pre-indexed biomedical corpora (eg Biorxiv, Medrxiv)
- Retrieve evidence fragment $e_{ij}$ and apply cosine similarity with original query to get $s_{ij}$
- Main supervisor looks at each evidence and decides whether to recommend that biomarker
- Also deduplicate and merge evidence trails

## Report Agent

- Recommend next biomarker(s) to take ordered by priority.
- Turn full output into detailed report. WITH CITATIONS.
