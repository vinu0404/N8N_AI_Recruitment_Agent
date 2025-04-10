#  Resume Screening Workflow – n8n

 - [Demo_Video_of_v1](https://drive.google.com/file/d/10_LuHV6t3m4SCRuGqvhMcsuMpdA1dKRD/view?usp=sharing)
-  [Demo_Video_of_v2](https://drive.google.com/file/d/1N9xcewCepLZBqRprVyHqf-Ddg92aqZOu/view?usp=sharing)
-  [Demo_Video_of_v3](https://drive.google.com/file/d/1YLW6zx0KERR87mzNRjKeXX8qzh-A0Fb3/view?usp=sharing)

This workflow automates the **resume screening process** using `n8n` and integrates with **AWS Bedrock** for summarization and evaluation of candidates against a job description.

##  Workflow Overview (in n8n)  

1. **Trigger Node**  
   - Type: Manual(in v1,v2) & Webhook(in v3) 
   - Starts the flow for a batch resume screening.

2. **Get Resume Data and Job Description**  
   - Format: .pdf files in Google Drive for Resume and .txt file for for Job Description.

3. **Summarizer & Evaluator Node**  
   - **Type**: AWS Bedrock (LLM: `arn:aws:bedrock:us-east-1::foundation-model/amazon.nova-micro-v1:0`)
   - **Prompt**: Custom summarizer prompt asking for:
     - Name  
     - Contact Info  
     - Educational Qualifications  
     - Job History  
     - Skill Set
     - Evaluates candidate's resume against the job description and returns:
     - Score (1–10) 


4. **Merge / Format Node**  
   - Combines summary and evaluation into structured output.

5. **Store or Output Node**  
   - Saves to Google Sheets.
  
  ### Steps from 1 to 5 are present in every version.

## Version 2 Updates

### Email Notifications (Partial)

- **To Recruiter**: 
  - Implemented functionality to send an email to the recruiter with a **table format** listing all the selected candidates.
  - This helps recruiters keep a record of whom they selected .

- **To Candidates**: 
  - Not implemented in this version.
  - Candidates do **not** receive any email notifications in Version 2.

 *This version focused on enhancing recruiter communication and tracking selections through structured email reports.*

---
- [Architecture]()

 ## Version 3 Updates

### New Features

- **AI-Powered Shortlisting**
  - The system now uses AI to automatically extract the **top K candidates** from the database based on their scores.
  - This saves time by allowing recruiters to focus only on the best-fit candidates instead of going through all resumes.

- **Recruiter Selection Interface**
  - A clean and interactive **web page** displays the top K shortlisted candidates.
  - Recruiters can **select candidates** directly from this list with checkboxes.

- **Email Notifications**
  - **To Candidates**: Automatically sends a personalized email to each selected candidate, informing them that they’ve been selected.
  - **To Recruiter**: Sends a confirmation email to the recruiter indicating that emails have been successfully sent to the selected candidates.

- **Webhook Integration**
  - A webhook is triggered when the recruiter confirms their selection.
  - The system uses this webhook to handle email delivery and track actions.

- **One-Click Workflow**
  - Everything is managed from a single page — fetch top K candidates, select, and trigger the email workflow with just a few clicks.

