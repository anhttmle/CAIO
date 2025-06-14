## Why Inject Domain Knowledge?

Artificial intelligence models are typically trained on large-scale internet data, which may not cover the specialized information required in certain industries or applications. This gap leads to three main challenges:

- **Lack of Specialization**: Generic internet data rarely includes the nuanced, domain-specific knowledge that subject-matter experts possess.
- **Uncertainty in Outputs**: Without domain anchors, AI-generated answers can be ambiguous or misleading.
- **High Cost of Correction**: Retrofitting or fine-tuning large language models (LLMs) with new data can be resource-intensive and time-consuming.

To enhance AI performance and reliability, we must identify inefficient processing steps and strategically inject domain knowledge provided by SMEs (Subject-Matter Experts).

---

## 1. Dev-Time Knowledge Injection

Integrating domain insights during development helps build a foundation for more accurate retrieval and reasoning later on. Two illustrative use cases are presented below:

### 1.1 Encoding Knowledge: Indexing COBOL Source Code

**Common Approach**
1. Summarize COBOL code into natural language descriptions using an LLM.
2. Chunk these summaries and convert each chunk into a vector embedding.
3. Store embeddings in a vector database for semantic retrieval.

**Heuristic (SME-Guided) Approach**
- **Reading Strategy**: Define where to begin in the source, which documentation to cross-reference, and how to traverse modules systematically.
- **Key Elements**: Identify module names, variable declarations, and coding conventions that signal important logic.
- **Dependency Detection**: Map relationships between programs, databases (schemas), and APIs using SME-driven rules rather than pure semantic similarity.

*Advantages*: This heuristic pipeline mirrors how COBOL analysts approach legacy code—improving relevance and reducing noise in indexed data.

---

### 1.2 Retrieving Knowledge: Contextual Search

**Common Approach**
1. Extract keywords from a user query and perform a database lookup.
2. Execute semantic (vector) search to find relevant text chunks.
3. Increase the retrieval `top_k` parameter to broaden context if initial results are insufficient.

**Heuristic (SME-Guided) Approach**
- **Multi-Source Integration**: Augment vector search with specialized tools like Jira for ticket histories or Google Drive for design docs.
- **Context Prioritization**: Use SME-provided heuristics to weight certain document types (e.g., architectural specs over meeting notes).

*Advantages*: Leveraging domain repositories beyond text embeddings yields higher precision and faster retrieval of critical information.

---

## 2. Runtime Knowledge Injection: Feedback API

Building feedback loops into production systems allows SMEs to continuously refine AI outputs in real time.

### Key Features of a Feedback API

- **Quality Voting**: SMEs (e.g., COBOL-E, COBOL-BA) can upvote or downvote generated responses to signal correctness.
- **Reference Tagging**: Experts can flag irrelevant or incorrect citations, improving future retrieval accuracy.
- **Guideline Annotations**: SMEs may attach corrective comments or guidelines (“This interpretation is incorrect; please follow X approach.”) that the assistant can incorporate dynamically.

By combining dev-time heuristics with runtime feedback, AI systems become progressively more aligned with domain best practices and expert expectations.
