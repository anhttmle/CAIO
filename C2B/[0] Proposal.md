# Transforming COBOL to Java

**Author:** NAL

**Date:** 2025-03-21

---

## 1. Abstract
Legacy COBOL systems, while robust and proven, face mounting challenges:
- **Maintenance & Talent Shortage**: The pool of skilled COBOL developers is rapidly shrinking.
- **High Operational Costs**: COBOL systems incur significant maintenance fees and can limit integration with modern technologies.
- **Business Agility**: Modern applications require flexible, scalable, and interoperable platforms.

=> Migrating to Java addresses these challenges by leveraging modern IDEs, rich third‑party libraries, and agile methodologies


## 2. Introduction

### a. Status Quo:

#### **Current Migration Process**
![CodeReader-Manual Process drawio](https://github.com/user-attachments/assets/05fe02fa-28bf-4c6d-8463-3264f8403eb9)

#### **Limitation**
Some costly workload of the current Process
- Understanding COBOL source code
- Developing on JAVA
- Build testcases & execute test base on the testcases (Manual & Automation)
- Communication
    - COBOL Engineer vs Business Analyst (JP)
    - Business Analyst (JP) vs Business Analyst (VN)
    - Technical Leader vs JAVA Engineer
    - Business Analyst (VN) vs Technical Leader/JAVA Engineer

=> We need automation. But the right question is: "How much automation should be implemented at any given time?

### b. State of AI Technology

#### How humans currently perform tasks?

- **System 1**: Fast, Intuitive base on patterns and experiences
![System_1](https://github.com/user-attachments/assets/c3c6860a-9348-483f-8580-d4ec3f6999dc)

- **System 2**: Slow, Analytical and Structured base on Planing, Reasoning and Optimization
![System 2](https://github.com/user-attachments/assets/dc128f92-970c-4f06-a60d-5eeebe372d41)

=> So we can aware that:
- LLM is like "System 1"
- Agentic AI is like "System 2"

#### Limitation of current AI Agent System
- Target Goal is fuzzy (text and depend on LLM)
- Guardrail Goal is heuristic & fuzzy (also Depend on LLM)
    - In/out format validation
    - Security in AI
    - Hallucination detection
- Memory:
    - Short-term memory
    - Long-term memory
      - Entity Memory
      - Procedure Memory
     
## 3. Approaches:
### a. By Level of Automation
- Level 0: Manual Testing/Control – No automation; humans do everything. (**Current Process**) 
- Level 1: Basic Machine Learning Automation – Simple tasks are automated with ML support.
- Level 2: Partial Autonomy – Some tasks are automated with human supervision still needed.
- Level 3: Conditional Autonomy – AI takes charge in defined scenarios but with human fallback.
- Level 4: High Autonomy – Minimal human supervision; systems can handle complex tasks.
- Level 5: Full Autonomy – AI systems operate entirely independently.
<img src="https://github.com/user-attachments/assets/e6d71f51-371f-439a-81f6-06ea784daf8c" alt="Level of Automation" width="500"/>

### b. By Iterative Improvement
- Carefully encode human experience into system.
- Human provide feedback after each step & iteration.
<img src="https://github.com/user-attachments/assets/68ecd5df-b128-4f6c-8135-79da1d798639" alt="Level of Automation" width="500"/>


## 4. Proposal solution & Roadmap:

### Proposal 1: AI as an Assistant – Targeting Costly Steps

#### Feasibility (Cautious approach)
- Automation: **Low** 
- Iterative Improvement: **Medium**

#### Description:
> This proposal focuses on leveraging AI as an assistant to enhance efficiency in the most resource-intensive steps of the COBOL-to-Java migration process. Instead of fully automating the workflow, AI tools will support human experts by automating repetitive and time-consuming tasks, improving communication, and reducing errors.

> By implementing low-level automation with medium iterative improvements, this approach ensures a cost-effective and low-risk transition while maintaining human oversight for critical decision-making.

#### Goal: 
Reducing manual work for current process (keeping humans in the loop for critical decisions).

#### Key Focus Areas:
1. COBOL Code Understanding → **AI-powered code summarization and analysis**.
    - Develop an AI-driven code summarizer that interprets legacy COBOL code and extracts business logic.
    - Integrate a chatbot interface for quick queries and clarifications.
    - Automatically generate documentation and code annotations for easier handover.

![CodeReader-P1 1 drawio](https://github.com/user-attachments/assets/bda054a3-2af0-4e84-ae38-2759e61a368b)

2. Java Development → **Automated unit test generation and partial code generation**.
    - Automate the generation of boilerplate code and unit tests for common functions.
    - Offer code refactoring suggestions to optimize performance and maintainability.
    - Implement a continuous feedback loop where human developers review AI-generated code.

![CodeReader-P1 2 drawio](https://github.com/user-attachments/assets/90d7da06-caee-4beb-ad65-1a01f0b6e63d)


3. Testing Process → **AI-supported test case creation and automation tools**.
    - Use AI to derive test cases from System Design & Business Requirements.
    - Auto-generate selenium script to execute automation test
    - Incorporate feedback mechanisms to refine test coverage over time.

![CodeReader-P1 3 drawio](https://github.com/user-attachments/assets/0ae95223-163e-498c-a2de-25c0cf9b474e)

4. Communication & Documentation → **AI-driven auto-translation and report generation to streamline collaboration between teams**.
   > COBOL Engineer vs Business Analyst (JP)
   > 
   > Business Analyst (JP) vs Business Analyst (VN)
   > 
   > Technical Leader vs JAVA Engineer
   > 
   > Business Analyst (VN) vs Technical Leader/JAVA Engineer

   - Employ AI-based translation tools for seamless cross-language communication (e.g., between JP and VN teams).
   - Auto take note design decisions, and documentation updates.
   - Set up a centralized dashboard to track project progress and document status.
  
![CodeReader-P1 4 drawio](https://github.com/user-attachments/assets/797d5187-14dd-4640-abb9-ea4780d3c49f)

#### Rough estimation:
- **Team**:
    - 1 PM/PO
    - 1 AI/ML specialist
    - 1-2 AI Engineer
    - 1-2 JAVA Engineer
    - COBOL Engineer (JP)
    - 1 QA Engineer
    - 1 BA
- **Cost**: 3-4 months/module

### Proposal 2: Agentic AI System with Human Supervision
#### **Feasibility**: Balanced approach
- Automation: **Medium**
- Iterative Improvement: **Medium**
#### Description:
> Integrate an agentic AI system that automates major tasks while retaining human supervision at key checkpoints.
> 
> This approach balances automation with quality control, reducing manual overhead without fully removing human oversight.

#### Goal: 
Automate tasks with human supervision.

#### Solutions:

![CodeReader-P2 drawio](https://github.com/user-attachments/assets/193b34bd-ddd9-4c81-b489-450de77dc9be)

#### Rough estimation:
- **Team**:
    - 1 PM/PO
    - 1 AI/ML specialist
    - 3 AI Engineer
    - 2 JAVA Engineer
    - COBOL Engineer (JP)
    - 1 QA Engineer
    - 1 BA
- **Cost**: 12 months

### Proposal 3: Fully Agentic AI System with Human Verification
#### **Feasibility**: Risky approach
- Automation: **High**
- Iterative Improvement: **High**
#### Description:
> Transition to a near–full AI-driven migration process where the AI independently handles most tasks and humans perform final verification.
>
> This approach maximizes automation, aiming for significant efficiency gains while ensuring quality through targeted human checks.
#### Goal:
Fully AI-driven migration with human verification.

#### Solution:

![CodeReader-P3 drawio](https://github.com/user-attachments/assets/1a2af1da-9b45-4610-9638-9e5e9a9ae0c0)

#### Rough estimation:
- **Team**:
    - 1 PM/PO
    - 1 AI/ML specialist
    - 1 AI/ML architecture
    - 5 AI Engineer
    - 3 JAVA Engineer
    - COBOL Engineer (JP)
    - 3 QA Engineer
    - 2 BA
- **Cost**: 18 months

### Roadmap
1. Understanding
   - Understanding JP's need
   - Working with VN team to understand current input/output
   - Define OKR
2. POC
3. Define Short-term plan & Long-term plan
4. Execution

### 

