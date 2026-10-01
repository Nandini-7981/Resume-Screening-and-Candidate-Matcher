<img width="1697" height="442" alt="Screenshot 2026-10-01 154757" src="https://github.com/user-attachments/assets/9b8c8bce-49fb-4214-9f7d-2ec8fad4ccf6" />
RESUME SCREENING AND CANDIDATE MATCHER
Project Documentation
Built with n8n, AI/LLM, and structured candidate data
1. Project Overview
Resume Screening and Candidate Matcher is an AI-powered recruitment automation project that helps recruiters analyze resumes against a job description. The workflow extracts resume information, compares the candidate's skills and experience with the job requirements, and produces a structured screening result.
2. Problem Statement
Recruiters may receive a large number of resumes for a single job opening. Manually reading and comparing every resume can take significant time. This project automates the initial screening process so that candidate information can be reviewed in a consistent, structured format.
3. Objectives
•	Accept job requirements and candidate resume information.
•	Extract useful text and candidate details from the resume.
•	Compare the resume with the job description using an AI/LLM model.
•	Identify matching skills, experience, and qualifications.
•	Highlight missing or weakly matched requirements.
•	Generate a structured screening result for recruiter review.
•	Reduce repetitive manual work in the initial screening stage.
4. Workflow
The n8n workflow can be organized into the following stages:
Start: Begins the manual resume screening workflow.
Job Inputs: Collects the job description, required skills, experience, education, and other job requirements.
Extract Resume Text: Receives or extracts the text/content of the candidate resume so it can be analyzed.
Screen Candidate: Sends the job requirements and resume information to the AI/LLM for candidate screening.
Screening Model: The AI model evaluates the relationship between the candidate profile and the job requirements.
Screening Result Parser: Converts the AI response into a structured result such as match summary, skills, gaps, and recommendation fields.
Format Result: Formats the final screening output so it is easy to read or store in Airtable/another database.
5. Candidate Matching Logic
The screening model should compare the candidate against the job description using factors such as:
•	Required technical skills
•	Preferred technical skills
•	Years and type of relevant experience
•	Education or certifications
•	Relevant projects and responsibilities
•	Keyword and skill alignment
•	Missing or unclear requirements
The AI output should be treated as an initial screening aid rather than a final hiring decision. A recruiter should review the resume and the generated result before making employment decisions.
6. Example Job Description
Job Title: Junior Software / AI Automation Engineer
Experience: 0–2 years
Required Skills: Python, APIs, automation, basic AI/LLM concepts, SQL
Preferred Skills: n8n, Airtable, GitHub, data processing
Responsibilities: Build automation workflows, work with APIs, process data, and support AI-based applications.
7. Example Screening Output
Field	Example
Candidate Name	Example Candidate
Matching Skills	Python, APIs, SQL, automation
Relevant Experience	1 year software/automation experience
Missing Skills	n8n experience not clearly shown
Education	B.Tech / relevant degree
Match Summary	Resume shows several skills relevant to the job description.
Recruiter Review	Review resume manually before proceeding.
8. n8n Workflow Components
•	Manual Trigger / Start: starts the workflow.
•	Edit Fields / Set: stores job description and candidate inputs.
•	Resume Text Extraction: prepares resume text for analysis.
•	Basic LLM Chain or AI Agent: sends the screening prompt to the selected AI model.
•	Structured Output Parser: converts the AI response into consistent fields.
•	Format Result: prepares the final result for display or database storage.
•	Airtable (optional): stores candidate details and screening results for tracking.
9. Suggested AI Screening Prompt
You are a resume screening assistant. Compare the candidate resume with the provided job description. Identify matching skills, relevant experience, missing requirements, and important observations. Return the result in a structured format with: candidate_name, matching_skills, relevant_experience, missing_requirements, education, match_summary, and recruiter_review_notes. Do not invent information that is not present in the resume.
10. Airtable Data Structure (Optional)
Column	Purpose
Candidate Name	Candidate identification
Email	Candidate contact information, if provided
Resume Text	Extracted resume content
Job Title	Position being screened
Matching Skills	Skills matching the job
Missing Requirements	Requirements not found or unclear
Match Summary	AI-generated comparison summary
Status	Recruiter review status
11. How to Run the Project
1.	Open the n8n workflow.
2.	Enter the job description and candidate resume information in the Job Inputs step.
3.	Run the workflow manually.
4.	Allow the resume text extraction step to prepare the candidate information.
5.	The Screen Candidate step sends the information to the AI/LLM.
6.	Review the parsed screening result.
7.	Store the result in Airtable if database tracking is enabled.
8.	A recruiter reviews the candidate before taking any hiring action.
12. Benefits
•	Saves time during initial resume review.
•	Creates a consistent screening format.
•	Makes candidate-to-job comparison easier.
•	Can be connected to Airtable for candidate tracking.
•	Can be extended to process multiple candidates.
•	Can be integrated with other recruitment automation workflows.
13. Limitations and Responsible Use
•	AI screening can make mistakes or misunderstand resume information.
•	A missing keyword does not necessarily mean a candidate lacks the skill.
•	The workflow should not be the sole basis for hiring or rejection decisions.
•	Recruiters should verify important qualifications directly from the resume and other appropriate sources.
•	Personal candidate data should be handled securely and only for legitimate recruitment purposes.
14. Suggested GitHub Repository Structure
resume-screening-candidate-matcher/
├── README.md
├── docs/
│   └── Project_Documentation.docx
├── workflow/
│   └── resume_screening_workflow.json
├── sample-data/
│   ├── sample_job_description.txt
│   └── sample_resume.txt
└── screenshots/
    └── n8n_workflow.png
15. Conclusion
The Resume Screening and Candidate Matcher demonstrates how n8n and AI can be combined to automate the first stage of resume analysis. The workflow takes job requirements and candidate information, uses an AI model to compare them, structures the result, and can optionally store the output in Airtable. The project can be extended with email notifications, multiple-candidate processing, scoring fields, dashboards, and other recruitment workflow integrations.
