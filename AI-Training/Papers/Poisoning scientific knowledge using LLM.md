# Poisoning Scientific Knowledge Using Large Language Models

> **Paper:** *Poisoning Scientific Knowledge Using Large Language
> Models*\
> **Authors:** Junwei Yang, Hanwen Xu, Srbuhi Mirzoyan, Tong Chen,
> Zixuan Liu, Wei Ju, Luchen Liu, Ming Zhang, Sheng Wang\
> **Preprint:** bioRxiv, posted November 10, 2023\
> **DOI:**
> [10.1101/2023.11.06.565928](https://doi.org/10.1101/2023.11.06.565928)\
> **Status:** The version analyzed in this note is a bioRxiv preprint
> and was not certified by peer review.

------------------------------------------------------------------------

## 1. Executive Summary

This paper studies whether large language models (LLMs) can be used to
create fabricated scientific abstracts that poison biomedical knowledge
graphs (KGs), ultimately manipulating downstream scientific
applications.

The authors introduce **Scorpius**, a conditional text-generation
framework that creates a malicious abstract around a selected
drug--disease relationship. The abstract is mixed with a large
collection of legitimate scientific papers. Existing
information-extraction systems may then extract the fabricated
relationship and add it to a biomedical KG. KG reasoning models can
propagate the effect of that false edge through the graph and assign an
artificially high relevance score to the selected drug.

The central finding is that **a single carefully constructed abstract
can substantially change drug rankings** in the experimental KG. The
paper reports that Scorpius moved 71.3% of evaluated drug--disease pairs
from outside the top 1,000 to the top 10 after adding one malicious
abstract.

The paper is not claiming that an LLM can make a drug biologically
effective. It demonstrates a vulnerability in a computational
knowledge-discovery pipeline: fabricated evidence can influence
extracted graph structure, learned representations, and downstream
rankings.

## 2. The Problem: How Scientific Knowledge Graphs Are Built

Biomedical knowledge graphs are used to organize facts extracted from
scientific literature. Typical entities include:

-   Drugs
-   Diseases
-   Genes

Relationships between entities are represented as graph edges. For
example:

``` text
Drug A --treats / is associated with--> Disease B
Drug A --targets---------------------> Gene C
Gene C  --associated with------------> Disease B
```

A typical KG-based scientific discovery pipeline has two stages.

### Stage 1: Knowledge graph construction

A collection of scientific papers is processed by relation-extraction
systems. The systems identify entities and relations in the text and
convert them into graph edges.

``` text
Scientific papers
       |
       v
Entity and relation extraction
       |
       v
Knowledge graph
```

### Stage 2: Knowledge graph reasoning

A KG reasoning model learns vector representations (embeddings) for
entities and relations. It uses these representations to estimate the
plausibility or relevance of relationships, including drug--disease
relationships that are not explicitly present in the graph.

``` text
Knowledge graph
       |
       v
KG representation learning
       |
       v
Drug–disease relevance scores
       |
       v
Ranked drug candidates
```

The pipeline therefore has two potential attack surfaces:

1.  **KG construction:** Can a malicious abstract cause a
    relation-extraction system to create a false edge?
2.  **KG reasoning:** If a false edge is inserted, can it substantially
    alter the scores or rankings produced by the reasoning model?

The paper investigates both.

## 3. Threat Model

The attacker wants a selected drug (the **promoting drug**) to appear
more relevant to a selected disease (the **target disease**) than it
should.

The attacker does not directly modify the KG, its extraction model, or
its reasoning model. Instead, the attacker creates a scientific-looking
abstract and relies on the normal literature-ingestion process to
introduce the abstract into the corpus.

The attack can be summarized as:

``` text
Attacker chooses a drug and a disease
                 |
                 v
       Generate a malicious abstract
                 |
                 v
       Mix it with legitimate papers
                 |
                 v
       Relation extraction identifies
          a fabricated relationship
                 |
                 v
       The KG gains a malicious edge
                 |
                 v
       KG reasoning is influenced
                 |
                 v
       The selected drug receives
       an artificially improved ranking
```

This is a **data poisoning** attack. The poisoned input is a document in
the source corpus; the attack takes effect when the normal pipeline
processes that document.

### Two attack settings

The paper defines two variants:

  -----------------------------------------------------------------------
  Setting                 Generator condition     Attacker's objective
  ----------------------- ----------------------- -----------------------
  Disease-specific        Promoting drug + target Increase the relevance
                          disease                 of one drug to one
                                                  target disease

  Disease-agnostic        Promoting drug          Increase the relevance
                                                  of one drug across
                                                  diseases
  -----------------------------------------------------------------------

The disease-agnostic setting is more challenging because a small number
of malicious relationships must influence the drug's relevance to many
diseases.

## 4. First Experiment: Vulnerability of KG Reasoning

Before developing Scorpius, the authors test whether KG reasoning models
are sensitive to the addition of a malicious edge.

### Experimental KG

The KG was constructed from **3,818,528 scientific papers** and
contained:

  Entity type     Number of entities
  ------------- --------------------
  Drugs                       16,468
  Diseases                     5,379
  Genes                       38,080

The authors evaluate three KG reasoning approaches:

-   **DistMult**
-   **ConvE**
-   **ComplEx**

They compare drug rankings before and after adding a malicious
drug--disease link.

### Disease-specific results

After adding one malicious link, the proportion of promoting drugs
receiving high rankings changed substantially:

  Ranking threshold     Before poisoning   After poisoning
  ------------------- ------------------ -----------------
  Top 1                             0.3%             48.2%
  Top 10                            1.9%             64.3%

All three reasoning methods were affected. The paper reports a larger
ranking impact for DistMult and ComplEx than for ConvE. The authors
suggest that ConvE's more shared parameterization makes it less
sensitive to an individual new link.

**Interpretation:** The reasoning stage can amplify the impact of a
single false relationship. A malicious edge does not merely appear as
one incorrect fact; it can alter the learned representation space and
influence the scores of candidate relationships.

### Disease-agnostic results

In the disease-agnostic setting, the authors add one, two, or three
malicious links and measure how the promoting drug's relevance changes
across diseases.

They observe that:

-   Adding more malicious links generally increases the drug's
    relevance.
-   The effect continues to increase as additional links are added.
-   The increase begins to converge at around ten links.
-   Some drugs can reach a top-10 ranking after only four malicious
    links in the reported experiment.

The authors also observe that some disease nodes are selected
repeatedly. These highly connected nodes act as **hub nodes**:
connecting a drug to a hub can influence its relevance to many other
diseases.

**Interpretation:** The structure of the KG matters. A strategically
selected edge connected to an influential node can have a broader effect
than an arbitrary edge.

## 5. Second Experiment: Vulnerability of KG Construction

The next question is whether a malicious abstract can actually cause an
existing relation-extraction system to extract the intended false
drug--disease relationship.

The authors randomly sample **2,000 drug--disease pairs that are not
connected** in the KG. For each pair, they attempt to create an abstract
that will cause the extraction pipeline to produce the desired link.

### Replacement-based approach

The initial approach starts from a real scientific abstract:

1.  Randomly select a real abstract.
2.  Replace the original drug and disease with the promoting drug and
    target disease.
3.  Randomly mask a proportion of words.
4.  Use a biomedical language model to fill the masked words.
5.  Run relation extraction and check whether the desired drug--disease
    link is recovered.

The study evaluates several relation-extraction approaches, including
GNBR, UIE, TDERR, and LUKE.

### Findings

The authors report that:

-   At least 30% of sampled pairs can be poisoned under the tested
    replacement settings.
-   A poisoning rate of at least 20% remains possible even when 60% of
    the words are randomly replaced.
-   The generated text can be unnatural, which motivates a more
    controlled generation method.

This experiment supports the premise that KG construction can be
vulnerable: a carefully modified abstract can sometimes pass through
existing extraction systems and introduce an intended relation.

## 6. Scorpius: The Proposed Poisoning Framework

Scorpius is designed to generate an abstract that satisfies two
competing goals:

1.  **Effectiveness:** The abstract should introduce a relationship that
    strongly changes the target drug's ranking.
2.  **Concealment:** The abstract should be less likely to be identified
    as malicious or rejected by the data-processing pipeline.

The framework has two major components:

-   Malicious-link selection
-   Malicious-abstract generation

### 6.1 Malicious-link selection

Given a promoting drug and, for the disease-specific setting, a target
disease, Scorpius identifies candidate nodes around the selected
entities and evaluates candidate links using two scores.

#### Poisonous score

The poisonous score estimates how much a candidate malicious link can
influence KG reasoning and improve the promoting drug's ranking.

The authors use an influence-function-inspired approach in the
disease-specific setting to estimate the impact of candidate links
without repeatedly retraining the full KG reasoning model for every
possible candidate.

Conceptually:

``` text
Candidate link
      |
      v
Estimate its influence on KG reasoning
      |
      v
Estimate ranking improvement
      |
      v
Poisonous score
```

A high poisonous score means that the link is expected to have a strong
downstream effect.

#### Concealing score

The concealing score estimates how suitable a candidate link is for
being hidden among legitimate relationships. It favors links that are
less likely to be detected or excluded by the defender.

Conceptually:

``` text
Candidate link
      |
      v
Estimate detectability / plausibility
      |
      v
Concealing score
```

Scorpius combines the poisonous and concealing scores to select a target
malicious link.

The important design idea is that the most influential link is not
necessarily the best attack choice if it is also easy to detect.
Scorpius balances impact with concealment.

### 6.2 Malicious abstract generation

After selecting a target link, Scorpius generates text intended to make
the relation extractor recover that link.

The generation process combines real scientific sentence structures,
ChatGPT, and biomedical language models.

#### Step 1: Build a sentence template

Scorpius finds a real scientific sentence that has been used to identify
the same relation type. It replaces the original drug and disease with
the promoting drug and target disease.

This creates a sentence template that preserves a relation pattern known
to work with the extraction system.

#### Step 2: Generate an abstract using ChatGPT

The paper uses the `gpt-3.5-turbo` API to expand the template into a
biomedical abstract.

ChatGPT is instructed to generate a scientific-style abstract while
retaining the target sentence.

However, the authors identify limitations in using ChatGPT output
directly:

-   It may not strictly preserve the required sentence or phrases.
-   General-purpose generation may not consistently match biomedical
    writing conventions.
-   API rate limits can make repeated generation slower.

#### Step 3: Refine the generation with BioBART

Scorpius uses the biomedical-domain model **BioBART** to refine the
generated text.

The paper describes two refinement strategies:

1.  Replace the context in the ChatGPT-generated abstract with a masked
    sentence template.
2.  Replace the ChatGPT generation with the original template, randomly
    mask nearby words, and use BioBART to fill the masks.

These strategies help preserve the desired relation while allowing the
surrounding text to be rewritten.

#### Step 4: Select the generation using perplexity

Scorpius generates candidate abstracts and uses **BioGPT perplexity** to
select the candidate with the lowest perplexity.

Perplexity measures how well a language model predicts a sequence of
tokens. In this context, lower perplexity is used as a proxy for text
that is more likely under a biomedical language model.

Important qualification: **lower perplexity does not establish
scientific correctness, truthfulness, or safety.** It is a fluency /
language-likelihood signal, not a fact-checking mechanism.

### Scorpius pipeline overview

``` text
Promoting drug + target disease
               |
               v
       Candidate node selection
               |
               v
   +---------------------------+
   | Evaluate candidate links  |
   |                           |
   | - Poisonous score         |
   | - Concealing score        |
   +---------------------------+
               |
               v
       Select malicious link
               |
               v
       Retrieve a real sentence
       with the required relation
               |
               v
       Replace drug and disease
       to create a sentence template
               |
               v
       Generate an abstract
       using ChatGPT (GPT-3.5)
               |
               v
       Refine with BioBART
       using masked templates
               |
               v
       Select candidate using
       BioGPT perplexity
               |
               v
       Malicious scientific abstract
```

## 7. Scorpius Evaluation

The authors compare Scorpius with:

-   **ChatGPT:** Direct abstract generation.
-   **Insertion approach:** A baseline that directly inserts the
    intended malicious link, representing an upper-bound-style reference
    for the impact of a successfully inserted link.
-   **Scorpius:** The proposed approach, which attempts to produce text
    that causes the extraction pipeline to create the intended link.

They evaluate the attack under low, medium, and high defensive settings.

### Disease-specific setting

Scorpius outperforms direct ChatGPT generation under the evaluated
defensive settings. Its performance is close to the direct-insertion
approach.

This indicates that Scorpius can generate abstracts that are not only
linguistically plausible according to the selected metric, but also
effective at inducing the desired relation in the KG pipeline.

### Disease-agnostic setting

Scorpius also outperforms ChatGPT in the disease-agnostic setting.
However, its performance is further from the direct-insertion baseline
than in the disease-specific setting.

This is consistent with the greater difficulty of influencing many
diseases through a small number of malicious links.

### Overall reported result

The paper's abstract reports that **71.3% of evaluated drug--disease
pairs were moved from outside the top 1,000 to the top 10 by adding one
Scorpius-generated malicious abstract**.

This is a result within the paper's experimental setup. It should not be
interpreted as a general success rate for arbitrary KGs, relation
extractors, or biomedical applications.

### Text fluency

The authors report that Scorpius-generated abstracts achieve better
BioGPT perplexity than ChatGPT-generated abstracts in both settings.

The result supports the authors' claim that Scorpius can generate text
that is more likely under the biomedical language model. It does not
prove that the text is factually credible or that human reviewers cannot
detect it.

## 8. Defense: Detecting Malicious Scientific Abstracts

The paper also develops a defender formulated as a **binary
classifier**:

``` text
Scientific abstract
        |
        v
  Malicious-abstract
     classifier
        |
        +------> Legitimate
        |
        +------> Malicious
```

The authors evaluate low, medium, and high defensive levels. Stronger
defense reduces the effectiveness of poisoning, but it also risks
incorrectly classifying legitimate relationships as malicious.

The paper emphasizes that conventional AI-generated-text detectors are
not sufficient for this problem. The defender needs to consider not only
whether a text looks machine-generated, but also how much the extracted
relationship would affect KG reasoning.

### The defense trade-off

  -----------------------------------------------------------------------
  Defensive level         Expected behavior       Main risk
  ----------------------- ----------------------- -----------------------
  Low                     Less aggressive         More malicious links
                          filtering               may remain

  Medium                  Stronger filtering      Some legitimate links
                                                  may be removed

  High                    More aggressive         Greater risk of
                          detection               degrading the KG by
                                                  rejecting true links
  -----------------------------------------------------------------------

The paper notes that the high defensive level can identify malicious
links effectively, but may also misclassify many real links and reduce
KG reasoning performance.

This is an important operational trade-off: maximizing attack detection
is not equivalent to maximizing the quality of the resulting knowledge
graph.

## 9. Main Contributions

The paper makes four main contributions.

1.  **Introduces scientific knowledge poisoning as a problem.** It
    studies how LLM-generated malicious scientific text can manipulate
    knowledge graphs and downstream applications.
2.  **Demonstrates vulnerabilities in both KG stages.** The experiments
    show that relation extraction can introduce malicious links and that
    KG reasoning can amplify their effects.
3.  **Proposes Scorpius.** The framework combines impact-aware link
    selection with controlled biomedical abstract generation.
4.  **Studies a defender.** The paper formulates malicious-abstract
    detection as a classification problem and demonstrates the trade-off
    between detecting attacks and preserving legitimate knowledge.

## 10. Limitations and Caveats

The authors explicitly identify several limitations.

### 10.1 Evaluation uses peer-reviewed articles

The experiments are performed using peer-reviewed articles. The authors
note that preprints may be more vulnerable because they are less likely
to have undergone the same level of editorial and peer review.

They propose investigating poisoning in preprint-based collections in
future work.

### 10.2 Defense can reject legitimate knowledge

The current defender can identify malicious links under the high
defensive setting, but it may also reject many real links. The authors
propose improving the defender with a supervised classifier.

### 10.3 Publication time is not modeled

The framework does not incorporate each paper's publication timestamp.
The authors suggest that emerging and highly visible topics may be more
attractive targets and propose incorporating time information in future
work.

### 10.4 Perplexity is not a truth metric

The use of BioGPT perplexity is a text-likelihood measure. It does not
verify whether the scientific claims are supported by experiments,
whether the cited evidence exists, or whether the proposed drug--disease
relationship is biologically valid.

### 10.5 Ranking changes are not biological validation

A drug moving up a KG-based ranking does not demonstrate clinical
efficacy, therapeutic benefit, or a causal biological relationship. The
experiments evaluate manipulation of a computational ranking pipeline.

### 10.6 Scope of the evidence

The paper is a proof-of-concept study using a particular biomedical KG,
extraction methods, and reasoning models. The reported numbers should
not be generalized automatically to all scientific KGs or production
knowledge-discovery systems.

## 11. Implications for RAG and Enterprise Knowledge Systems

The paper focuses on scientific KGs, not retrieval-augmented generation
(RAG). Nevertheless, its threat model has useful parallels with
document-based enterprise AI systems.

### Similarity

Both architectures depend on external information being ingested and
later used by downstream models:

``` text
Scientific KG pipeline             RAG pipeline
----------------------             -------------
Papers                              Documents
  |                                   |
Extraction                          Parsing / chunking
  |                                   |
Knowledge graph                     Search index
  |                                   |
KG reasoning                        Retrieval + reranking
  |                                   |
Drug ranking                        LLM answer
```

In both cases, a malicious or low-quality source can influence
downstream outputs.

### Important difference

In the paper, the malicious abstract can change the KG structure and the
embedding space learned by the KG reasoning model.

In a conventional RAG system, adding a malicious document usually does
**not** modify the LLM's model weights. Its influence generally occurs
through retrieval: the document may be retrieved, placed in the prompt,
and used by the LLM to generate an answer.

The distinction matters because the mitigation points differ.

### Practical defenses for RAG and knowledge platforms

The following are architectural recommendations derived from the paper's
threat model; they are not experiments reported by the authors.

  -----------------------------------------------------------------------
  Layer                   Recommended control     Purpose
  ----------------------- ----------------------- -----------------------
  Source ingestion        Source allowlists,      Establish where
                          publisher / owner       information came from
                          identity, provenance    
                          metadata                

  Document validation     Malware checks, format  Reduce unsafe or
                          validation, duplicate   low-quality inputs
                          detection,              
                          suspicious-content      
                          screening               

  Knowledge extraction    Evidence spans,         Make extracted facts
                          entity-resolution       auditable
                          checks, relation        
                          confidence, schema      
                          validation              

  Knowledge graph         Track edge provenance,  Avoid treating every
                          source count,           edge as equally
                          timestamps, and         trustworthy
                          confidence              

  Retrieval               Source-aware ranking,   Reduce the chance that
                          trust filters,          untrusted content
                          freshness controls      dominates context

  Answer generation       Require citations and   Make outputs traceable
                          evidence-grounded       to source material
                          claims                  

  Monitoring              Detect unusual changes  Identify downstream
                          in rankings, retrieval  effects of newly
                          frequency, or entity    ingested data
                          relationships           

  Governance              Review workflows,       Support investigation
                          rollback, versioning,   and recovery
                          and audit logs          
  -----------------------------------------------------------------------

### A useful design principle

Do not evaluate ingestion quality only by asking whether a document can
be parsed or whether an extracted relation has a high model confidence.

Also ask:

> **How much can this document change the downstream system's
> decisions?**

For example, a newly ingested document that causes a previously
irrelevant entity to become the top recommendation deserves more
scrutiny than a document that adds a low-impact fact.

This suggests an **impact-aware ingestion pipeline**:

``` text
New document
     |
     v
Parse and extract candidate facts
     |
     v
Validate source and evidence
     |
     v
Estimate downstream impact
     |
     +---- Low impact ----> Normal ingestion
     |
     +---- High impact ---> Additional review
                              |
                              v
                        Approve / reject
                              |
                              v
                     Versioned ingestion
                     with rollback support
```

## 12. Critical Takeaways

1.  **The attack targets the data pipeline, not the LLM weights.** The
    attacker manipulates the corpus from which structured knowledge is
    extracted.
2.  **A single edge can have a disproportionate effect.** KG reasoning
    can propagate the effect of a false relationship through learned
    embeddings.
3.  **Text generation and graph impact must be optimized together.**
    Scorpius considers both the downstream influence of a link and the
    likelihood that it will pass detection.
4.  **Fluency is not truth.** Lower perplexity makes text more probable
    under a language model; it does not make the scientific claim valid.
5.  **Defenses must consider downstream impact.** Detecting AI-generated
    text alone is insufficient, and aggressive filtering can remove
    legitimate knowledge.
6.  **The same principle applies to RAG.** Trust, provenance, evidence,
    impact monitoring, and rollback should be part of the ingestion
    architecture.

## 13. Questions for Further Study

-   How can a KG system estimate the marginal impact of each newly added
    edge without retraining the entire reasoning model?
-   Can provenance-aware KG reasoning reduce the influence of facts
    supported by only one low-trust source?
-   How should a system distinguish a genuinely novel scientific
    discovery from a strategically influential but weakly supported
    claim?
-   Can retrieval systems estimate the downstream impact of a document
    before allowing it to influence answers?
-   How can defenses balance false-positive and false-negative rates
    when rejecting suspicious knowledge?
-   What changes when the source corpus includes preprints, web pages,
    patents, or automatically generated documents?

## 14. Reference

Yang, J., Xu, H., Mirzoyan, S., Chen, T., Liu, Z., Ju, W., Liu, L.,
Zhang, M., & Wang, S. (2023). *Poisoning Scientific Knowledge Using
Large Language Models*. bioRxiv preprint.

-   DOI: https://doi.org/10.1101/2023.11.06.565928
-   Source: https://www.biorxiv.org/content/10.1101/2023.11.06.565928v1
