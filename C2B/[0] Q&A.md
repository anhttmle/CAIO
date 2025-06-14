## 0. Providing 3rd API key for development
- LLM: OpenAI API key (https://platform.openai.com/api-keys)
- ReRanker: Cohere API key (https://dashboard.cohere.com/welcome/login?redirect_uri=%2Fapi-keys)
## 1. Who will use the Assistant?
- COBOL-E (Cobol Engineer) – Required: Responsible for reviewing specifications to ensure they align with the logic implemented in the source code.
- COBOL-BA (Business Analyst for Cobol projects) – Required: Provides the documentation template and ensures that specifications reflect the correct business logic.
- JAVA-BA (Business Analyst for Java migration) – Optional: Supports the migration effort from a business analysis perspective.
- JAVA-E (Java Engineer for Java migration) – Optional: Develops the new Java-based solution.
- JAVA-PO (Product Owner for Java migration) – Optional: Oversees the migration project and sets priorities.
- JAVA-TL (Technical Lead for Java migration) – Optional: Designs the architecture and guides technical implementation.
- Admin/Operator – Optional: Manages configuration and operation of the Assistant.

## 2. What documentation template is used for COBOL-based project specs?
> (JP side responsible for providing this)

## 3. What are the obstacles preventing JAVA-BA and JAVA-E from fully understanding the specs?
> (VN side to provide insights)
  
## 4. Can you describe how a typical COBOL-E reads and analyzes the source code?
> (Seeking domain knowledge of COBOL-E)
- CALL -> execute external module
- PERFORM -> execute internal COBOL file
- COBOL file name stand for biz feature

## 5. Once the product is complete, how will it be used?
  - Option 1: Upload repositories to generate specs and interact via chat
    - Upload a single repository
    - Upload multiple repositories
  - Option 2: Add various supplementary documents to describe the entire system, then generate specs and chat with the Assistant
