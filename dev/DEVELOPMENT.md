# Development notes

---

**Objectives**

1. Re-implement pipeline from research paper
2. Benchmark and test variations of the pipeline to achieve the original objective
3. Apply the same pipeline structure for a new objective



# Pipeline structure

**One crew consisting of...**

1. Scoping agent
2. Data Scientist agent
3. Research Supervisor agent
4. Reporting agent

We will define the following tasks

1. Engage in dialogue with user and clarify patient constraints, demographics, medical data, readings to generate B1 (scoping agent, no tools)
2. Parse this information to a data scientist so that they can search databases for this info (scoping agent, no tools)

3. Identify datasets that contain the following information and will provide us with info (data analysis agent, tools: access to database)
4. Out of the features in the datasets, identify the best ones to filter the dataset by (data analysis agent, tools: access to database)
5. Filter the datasets and collate them all (data analysis agent, tools: Dataset parsing, merging, filtering, manipulation)
6. Get summary statistics from the dataset and visualise with exploratory data analysis (data analysis agent, tools: EDA?)
7. Preprocess data- standardise, normalise, split into training/testing/validation, hyperparams maybe? (data analysis agent, tools: dataset manipulation)
8. Apply various ML algorithms and find the best model with the lowest loss - ensuring it generalises well (data analysis agent or none, tools: AutoML)

9. Order input features by importance from this model (no agent, tools: AutoML/maths/logic/custom function)

10. For each feature, generate a suitable query and research strategy (agent: Research, tools: None)

11. Dynamically create a new task for each query to perform RAG on knowledge base and return each piece of evidence (with source) and embedding (agent: None, tools: RAG)

12. Deduplicate RAG knowledge base so only unique pieces of info are considered (agent: Research, tools: None)

13. Compute similarity matrix (agent: None, tools: Custom similarity function)

14. Collect all high similarity points from the similarity matrix and merge into 1 collection per biomarker (agent: Research, tools: None)
15. Read evidence for each query and consider similarity score to classify whether each biomarker/query is novel or established (agent: Research, tools: None)

16. Given collections of novel and established biomarkers (as well as their sources and similarity scores), create a report with citations (agent: Reporting, tools: None)
