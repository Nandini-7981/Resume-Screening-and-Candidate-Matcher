# Resume Screening & Candidate Matching Workflow

An AI-powered workflow that screens a candidate's resume against a job description and returns a structured match result. It is built as a low-code automation workflow (n8n-style canvas) using an LLM chain with a structured output parser.

---

## Overview

Manual resume screening is slow and inconsistent. This project automates the first-pass review by:

1. Taking a job description and requirements as input
2. Taking the candidate's resume text as input
3. Asking an LLM to compare the two and produce a structured evaluation
4. Formatting the result into a clean, readable output

---

## Workflow Architecture

```
Start → Job Inputs → Extract Resume Text → Screen Candidate → Format Result
                                              ├── Screening Model (LLM)
                                              └── Screening Result Parser
```

| Node | Type | Purpose |
|------|------|---------|
| **Start** | Manual trigger | Starts the workflow on demand |
| **Job Inputs** | Set / Edit Fields | Holds the job title, description, required skills, and experience |
| **Extract Resume Text** | Set / Edit Fields | Holds (or extracts) the candidate's resume text |
| **Screen Candidate** | LLM Chain | Sends job + resume data to the model with a screening prompt |
| **Screening Model** | Chat model (OpenAI) | The language model attached to the chain |
| **Screening Result Parser** | Structured Output Parser | Forces the model's response into a fixed JSON schema |
| **Format Result** | Set / Edit Fields | Cleans up and shapes the final output |

---

## Features

- Resume-to-job matching with an overall match score
- Strengths, gaps, and missing skills identified per candidate
- Consistent, structured JSON output (no free-form parsing)
- Easy to modify: change the prompt, model, or schema without code
- Extendable to batch screening, email, ATS, or spreadsheet integrations

---

## Prerequisites

- [n8n](https://n8n.io/) (self-hosted or cloud)
- An OpenAI API key (or another supported chat model provider)
- A job description and a candidate resume (as text)

---

## Setup

1. **Import the workflow**
   - Open n8n → *Workflows* → *Import from file*
   - Select `workflow.json` from this repository
2. **Add credentials**
   - Open the **Screening Model** node
   - Create/select your OpenAI credential and paste your API key
3. **Configure inputs**
   - In **Job Inputs**, fill in the job title, description, and requirements
   - In **Extract Resume Text**, paste the resume text (or connect a file/PDF extraction node)
4. **Run**
   - Click **Execute Workflow** and review the output of **Format Result**

---

## Inputs

**Job Inputs**

| Field | Description |
|-------|-------------|
| `job_title` | Role being hired for |
| `job_description` | Full job description |
| `required_skills` | Must-have skills |
| `experience_required` | Minimum experience level |

**Extract Resume Text**

| Field | Description |
|-------|-------------|
| `resume_text` | Plain text content of the candidate's resume |

> Field names are suggestions. Match them to the ones used in your workflow.

---

## Output Schema (Example)

The **Screening Result Parser** enforces a structure like this:

```json
{
  "candidate_name": "Jane Doe",
  "match_score": 82,
  "recommendation": "Shortlist",
  "matched_skills": ["Python", "SQL", "Data Analysis"],
  "missing_skills": ["Kubernetes"],
  "strengths": ["5 years relevant experience", "Strong analytics background"],
  "concerns": ["No cloud deployment experience"],
  "summary": "Strong fit for the role with minor skill gaps."
}
```

---

## Example Screening Prompt

```
You are an experienced technical recruiter.
Compare the candidate's resume to the job requirements below.

Job Title: {{ job_title }}
Job Description: {{ job_description }}
Required Skills: {{ required_skills }}

Resume:
{{ resume_text }}

Evaluate the candidate objectively using only the information provided.
Return a match score (0-100), matched and missing skills, strengths,
concerns, and a final recommendation.
```

---

## Customization Ideas

- Add a **PDF/DOCX extraction** node to read resume files automatically
- Loop over multiple resumes for **batch screening** and rank candidates
- Write results to **Google Sheets, Airtable, or an ATS**
- Send shortlisted candidates an email automatically
- Swap the model (OpenAI, Anthropic, Gemini, local LLM) in the model node

---

## Responsible Use

AI screening should **assist**, not replace, human judgment.

- Always have a human review the final hiring decision
- Avoid including protected attributes (age, gender, ethnicity, etc.) in prompts
- Test for bias and validate results regularly
- Follow local hiring and data-privacy regulations when storing resumes

---

## Repository Structure

```
.
├── README.md
├── workflow.json        # Exported workflow
├── screenshots/
│   └── workflow.png     # Canvas screenshot
└── samples/
    ├── job_description.txt
    └── sample_resume.txt
```

---

## Roadmap

- [ ] Batch resume processing and ranking
- [ ] File upload / PDF parsing
- [ ] ATS and email integrations
- [ ] Scoring rubric customization

---

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License

Distributed under the MIT License. See `LICENSE` for details.
