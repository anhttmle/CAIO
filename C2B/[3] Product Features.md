
# 1. Configuration
- Currently we only support using openAI models
<img width="317" alt="image" src="https://github.com/user-attachments/assets/bcf93f8b-3248-432e-b524-96d7cc7716f9" />

# 2. Authorization
- User can login and using as separate session, also help clarify feedback among users
<img width="1557" alt="image" src="https://github.com/user-attachments/assets/82ef650f-e4ee-4335-b945-ff99faae209f" />

# 3. Indexing data
   - Upload/Index Cobol Repo (Zip file)
<img width="312" alt="image" src="https://github.com/user-attachments/assets/0419c1e0-3a23-43e6-ba84-a125a72c50f1" />

   - Summarize (Backend)
   - Chunking (Backend)
   - Semantic Storing (Backend)

   - Delete Indexed data
<img width="335" alt="image" src="https://github.com/user-attachments/assets/2705141e-3a25-4a8a-a5c7-ffd4ad77104a" />



   - Visualize Indexing Status
<img width="303" alt="image" src="https://github.com/user-attachments/assets/190a9ab2-f0af-4d50-8516-b675e7517f69" />


# 4. Answer Generation
- Generate data base on user question
<img width="1224" alt="image" src="https://github.com/user-attachments/assets/ccf17aaf-cb73-493a-a542-31511f860df1" />

# 5. Feedback
### A. Tag on Reference
- Users can label references as relevant or irrelevant.
<img width="481" alt="image" src="https://github.com/user-attachments/assets/c825d36f-b078-4344-a968-5b783aad0128" />

> Helps us adjust the way to index & retrieve data for Assistant to choose better context next time.

### B.👍 Up Vote / 👎 Down Vote on Assistant’s Answer

- Up vote/Down vote:
<img width="1207" alt="image" src="https://github.com/user-attachments/assets/d529c721-e738-4bbe-94a2-48bda3d5affd" />

> Help measuring accuracy of Assistant

- Quick way to rate the overall helpfulness of the response:
<img width="393" alt="image" src="https://github.com/user-attachments/assets/898684ae-80aa-4bca-be02-346d557dcaaa" />

> Useful for automated performance tracking.

~~C. 💬 Add Comment on Reference ➝ feeds Few-shot Prompt~~


### D. 💬 Add Comment on Answer ➝ feeds Few-shot Prompt
<img width="470" alt="image" src="https://github.com/user-attachments/assets/0faf4a26-0850-421f-80a8-90b0eb8f71f5" />

> Users can explain what the Assistant got wrong or right. We use these comments to tune prompt to help Assistant behave in similar future cases.
