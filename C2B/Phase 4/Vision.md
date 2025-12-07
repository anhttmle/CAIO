<h1 style="text-align:center;">Restructure-AI (ReAI) Vision</h1>

## A. Ultimate Goal
Restructure-AI (**ReAI**) system **centralizes work-load from transforming legacy projects** like COBOL to modern ones
Some main features that ReAI can have to assist human on the transformation

- ReAI help analyze source code COBOL to **build up projects specs** (_Phase 1-2-3_)
- ReAI help providing answer through **Q&A about source code, biz, calendar, roadmap, workload, progress,...**
- ReAI can be **fit into ecosystem of software development** (calendar, project management, issue tracking, ...)  => ReAI will treat them as tools to call
- ReAI will **collab with humans**
  - ReAI **plans** & **executes**
  - Human provide **domain knowledge**, **review** result from ReAI and make **adjustment**
  
## B. ReAI collaborates tighly with humans
- Like proposal from [Phase 1](https://github.com/anhttmle/CAIO/blob/main/C2B/%5B0%5D%20Proposal.md#a-by-level-of-automation)
- In ReAI, instead of build unique workflow we **should build multiple level of automation & collaboration between AI <-> Humans**
  - **Level 0**: Humans **manually** do everything
    > **ReAI provide editor so user can manually do their job**
  - **Level 1**: Humans get **recommendation from AI** when **manually** doing their work
    > **ReAI automatically provides recommendation when user manually operate on editor**
  - **Level 2**: Humans request AI to do some specific piece of work and humans reviews/adjusts the result
    > **User request ReAI zoom-in on specific section or node in a diagram**
  - **Level 3**: Human let AI do a complex work and reviewing step by step
    > **ReAI preparing summarization for each source code file & user select groups of context/file & ReAI generating overview of the group**
  - **Level 4**: Human let AI do a complex work and reviewing final result
    > **ReAI automatically generating specs/wiki & back to user review**
- And will apply to each component of ReAI. Such as:
  - **Documentization** for **Cobol Engineer**, **BA**: Understanding legacy project source code to preparing documents (specs/wiki)
  - **Planing** for **Product Owner/Director**: short-term  & long-term plan for the transformation
    - Long-term: preparing vision & roadmap for the transformation
    - Short-term: Scoping workload, task and preparing backlog
  - **Management** for **Project Owner/Manager**: distributing workload, tracing progress & raise alert on any potential delay or risk of quality by integrating with software development tools (calendar, project management, issue tracking)
  - **Development** for **Java Developer**: from the plan and backlog, gradually develop new system by integrating with AI code like Cursor/Claude Code/...
  - **Testing** for **Tester/QA/QC**: beside CI/CD, ReAI provide testing report by collaborate with Tester  

<img width="1261" height="1501" alt="Proposal-Mockup-Vision" src="https://github.com/user-attachments/assets/17c2fbe6-e932-437f-8b3e-e1163cfa5f32" />


