#  Resume Screening Workflow – n8n

[Demo_Video_of_v1](https://drive.google.com/file/d/10_LuHV6t3m4SCRuGqvhMcsuMpdA1dKRD/view?usp=sharing)

This workflow automates the **resume screening process** using `n8n` and integrates with **AWS Bedrock** for summarization and evaluation of candidates against a job description.

##  Workflow Overview (in n8n)

1. **Trigger Node**  
   - Type: Manual 
   - Starts the flow for a batch resume screening.

2. **Get Resume Data and Job Description**  
   - Format: .pdf file in Google Drive for Resume and .docs file for for Job Description.

3. **Summarizer & Evaluator Node**  
   - **Type**: AWS Bedrock (LLM: `mistral.mixtral-8x7b-instruct-v0:1`)
   - **Prompt**: Custom summarizer prompt asking for:
     - Name  
     - Contact Info  
     - Educational Qualifications  
     - Job History  
     - Skill Set
     - Evaluates candidate's resume against the job description and returns:
     - Score (1–10)  


5. **Merge / Format Node**  
   - Combines summary and evaluation into structured output.

6. **Store or Output Node**  
   - Saves to Google Sheets.

## Prompt Template

Used in both LLM nodes (Summarizer & Evaluator)
