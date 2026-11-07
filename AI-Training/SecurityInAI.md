# 1. AI development lifecycle

<img width="925" height="234" alt="image" src="https://github.com/user-attachments/assets/ef88349c-0e17-4bbb-ad60-7a2fb1ccaf4b" />



```mermaid

  graph TD
  owner["Owner"] --> model(("Model"))
  user["User"] --> model
  partner["Partner"] --> model
  community["Community"] --> model
  operator["Operator"] --> model
  

```


# 2. Security in AI

### Data poisoning
> Data poisoning happens when an attacker intentionally modifies or injects malicious data into a training dataset to influence the model's behavior.

There are two important categories:
- **Availability poisoning**: Degrades overall model performance.
- **Targeted poisoning**: Causes specific inputs or situations to produce attacker-desired predictions.

### Backdoor attacks
> A backdoor attack is a special type of poisoning attack in which an attacker trains a model to behave normally under ordinary conditions but behave maliciously when a specific trigger appears.

### Model extraction and model theft
> An attacker attempts to reconstruct or approximate a proprietary model by querying its API and observing the outputs.

### Model inversion and membership inference
> These attacks attempt to extract sensitive information from a trained model.
> **Inversion**: An attacker uses model outputs to infer information about training data.
> **Membership**: An attacker tries to determine whether a particular record was included in the model's training dataset.

### Model supply-chain attacks
> AI models depend on many external components:
> - Pretrained models.
> - Open-source datasets.
> - Python packages.
> - Training frameworks.
> - Third-party plugins.
> - Model repositories.
> 
> An attacker may compromise one of these dependencies.



# 3. Poisoning Scientific Knowledge Using Large Language Models

## A. Overview
> The authors introduce Scorpius, a conditional text-generation framework that creates a malicious abstract around a selected drug--disease relationship.
>
> It demonstrates a vulnerability in a computational knowledge-discovery pipeline: fabricated evidence can influence extracted graph structure, learned representations, and downstream rankings.

## B. The Problem: How Scientific Knowledge Graphs Are Built
> Biomedical knowledge graphs are used to organize facts extracted from scientific literature. Typical entities include:
> - Drugs
> - Diseases
> - Genes

A typical KG-based scientific discovery pipeline has two stages.

**Stage 1**: Knowledge graph construction
> A collection of scientific papers is processed by relation-extraction systems. The systems identify entities and relations in the text and convert them into graph edges.

```mermaid

  graph TD
  papers["Scientific papers"] --> matterial["Entity and relation extraction"]
  matterial --> kg["Knowledge graph"]

```

**Stage 2**: Knowledge graph reasoning
> A KG reasoning model learns vector representations (embeddings) for entities and relations. It uses these representations to estimate the plausibility or relevance of relationships, including drug--disease relationships that are not explicitly present in the graph.

```mermaid

  graph TD
  kg["Knowledge graph"] --> representation["KG representation learning"]
  representation --> score["Drug–disease relevance scores"]
  score --> rank["Ranked drug candidates"]

```

**The pipeline therefore has two potential attack surfaces:**
1. **KG construction**: Can a malicious abstract cause a relation-extraction system to create a false edge?
2. **KG reasoning**: If a false edge is inserted, can it substantially alter the scores or rankings produced by the reasoning model?

## C. Threat Model
> The attacker wants a selected drug (the promoting drug) to appear more relevant to a selected disease (the target disease) than it should.
>
> The attacker does not directly modify the KG, its extraction model, or its reasoning model. Instead, the attacker creates a scientific-looking abstract and relies on the normal literature-ingestion process to introduce the abstract into the corpus.

```mermaid

  graph TD
  s1["Attacker chooses a drug and a disease"] --> s2["Generate a malicious abstract"]
  s2 --> s3["Mix it with legitimate papers"]     
  s3 --> s4["Relation extraction identifies a fabricated relationship"]       
  s4 --> s5["The KG gains a malicious edge"]       
  s5 --> s6["KG reasoning is influenced"]
  s6 --> s7["The selected drug receives an artificially improved ranking"]       

```

> This is a data poisoning attack. The poisoned input is a document in the source corpus; the attack takes effect when the normal pipeline processes that document.

**Two attack settings**:
- **Disease-specific**: Promoting drug + target. Increase the relevance disease of one drug to one target disease
- **Disease-agnostic**: Promoting drug. Increase the relevance of one drug across diseases

## D. Vulnerability of KG Reasoning
> Before developing Scorpius, the authors test whether KG reasoning models are sensitive to the addition of a malicious edge.

**Experimental KG:**
- The KG was constructed from 3,818,528 scientific papers and contained:
  | Entity type | Number of entities |
  |------|------------|
  | Drugs | 16,468 |
  | Diseases | 5,379 |
  | Genes | 38,080 |

- The authors evaluate three KG reasoning approaches:
  - DistMult
  - ConvE
  - ComplEx
- They compare drug rankings before and after adding a malicious drug--disease link.
  | Setting | Action | Result |
  |------|------|------------|
  | Disease-specific results | adding one malicious link | Top 1: 0,3% -> 48,2% <br> Top 10: 1,9% -> 64,3%|
  | Disease-agnostic | add one, two, or three malicious links and measure how the promoting drug's relevance changes across diseases | - Adding more malicious links generally increases the drug's relevance. <br> The effect continues to increase as additional links are added. <br> - The increase begins to converge at around ten links. <br> - Some drugs can reach a top-10 ranking after only four malicious links in the reported experiment. |

> The authors also observe that some disease nodes are selected repeatedly. These highly connected nodes act as hub nodes: connecting a drug to a hub can influence its relevance to many other diseases.

## E. Vulnerability of KG Construction
> The authors randomly sample 2,000 drug--disease pairs that are not connected in the KG. For each pair, they attempt to create an abstract that will cause the extraction pipeline to produce the desired link.

**Replacement-based approach**: The initial approach starts from a real scientific abstract
1. Randomly select a real abstract.
2. Replace the original drug and disease with the promoting drug and target disease.
3. Randomly mask a proportion of words.
4. Use a biomedical language model to fill the masked words.
5. Run relation extraction and check whether the desired drug--disease link is recovered.

> The study evaluates several relation-extraction approaches, including GNBR, UIE, TDERR, and LUKE.

**Result**:
- At least 30% of sampled pairs can be poisoned under the tested replacement settings.
- A poisoning rate of at least 20% remains possible even when 60% of the words are randomly replaced.
- The generated text can be unnatural, which motivates a more controlled generation method.

## F. Scorpius: The Proposed Poisoning Framework
- Scorpius is designed to generate an abstract that satisfies two competing goals:
  - **Effectiveness**: The abstract should introduce a relationship that strongly changes the target drug's ranking.
  - **Concealment**: The abstract should be less likely to be identified as malicious or rejected by the data-processing pipeline.
- The framework has two major components:
  - Malicious-link selection
  - Malicious-abstract generation


## G. Scorpius Evaluation

## H. Defense: Detecting Malicious Scientific Abstracts

## I. Main Contributions

## J. Limitations and Caveats
