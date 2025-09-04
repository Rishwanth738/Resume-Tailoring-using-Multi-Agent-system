# Automated Job Application Assistant with crewAI

This repository contains a powerful multi-agent system built with **crewAI** designed to automate and tailor the job application process for tech roles. By providing a job posting URL, a GitHub profile, and a personal summary, this "crew" of AI agents collaborates to produce a resume tailored specifically for the job and a set of custom interview preparation materials.

## 🚀 Overview

The project simulates a team of four specialized AI agents that work in concert to streamline job applications. It showcases how `crewAI` can orchestrate complex workflows, manage dependencies between tasks, and leverage both external and local data sources to produce high-quality, contextualized output.

### Key Features:
- **Four Specialized AI Agents:** A researcher, a personal profiler, a resume strategist, and an interview preparer, each with a unique role.
- **Advanced Tool Integration:** Utilizes tools for web scraping (`ScrapeWebsiteTool`), internet search (`SerperDevTool`), and local file analysis (`FileReadTool`, `MDXSearchTool`).
- **Parallel Task Execution:** The initial research on the job posting and the candidate profile runs asynchronously for maximum efficiency.
- **Task Dependency Management:** Later tasks, like resume tailoring, intelligently wait for the completion of prerequisite tasks before they begin.
- **Generates Two Key Deliverables:**
    1.  A `tailored_resume.md` file, customized to match the job description.
    2.  An `interview_materials.md` file with relevant questions and talking points.

---

## 🏛️ How It Works: The Workflow

The crew follows a structured, multi-step process to generate the application materials:

1.  **Parallel Research (Async):**
    * The **Tech Job Researcher** agent analyzes the provided job posting URL to extract key skills, qualifications, and experiences required.
    * Simultaneously, the **Personal Profiler** agent analyzes the candidate's GitHub profile, resume file (`fake_resume.md`), and personal write-up to create a comprehensive professional profile.

2.  **Resume Tailoring:**
    * Once both research tasks are complete, the **Resume Strategist** agent takes the job requirements and the candidate's profile as context. It then strategically revises the resume to highlight the most relevant skills and experiences that align perfectly with the job posting.

3.  **Interview Preparation:**
    * Finally, after the tailored resume is created, the **Interview Preparer** agent uses the job requirements, the candidate's profile, *and* the newly tailored resume to generate a list of likely interview questions and strategic talking points.

---

## 🔧 Getting Started

Follow these steps to set up and run the project on your local machine.

### Prerequisites

- Python 3.9 or higher
- Git

### 1. Clone the Repository

```bash
git clone [https://github.com/your-username/your-repository-name.git](https://github.com/your-username/your-repository-name.git)
cd your-repository-name
```

### 2. Create a Virtual Environment

It's highly recommended to use a virtual environment to manage dependencies.

```bash
python -m venv venv
source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
```

### 3. Install Dependencies

Install the required libraries directly using pip.

```bash
pip install crewai==0.28.8 crewai_tools==0.1.6 langchain_community==0.0.29 langchain_openai python-dotenv ipykernel jupyter
```

### 4. Configure API Keys

The project requires API keys for OpenAI (for the LLMs) and Serper (for search capabilities).

Create a file named `.env` in the root of your project directory and add your keys as follows:

```
# .env file
OPENAI_API_KEY="your_openai_api_key"
SERPER_API_KEY="your_serper_api_key"
OPENAI_MODEL_NAME="gpt-3.5-turbo" # Or gpt-4-turbo if you have access
```

### 5. Add Your Resume

Make sure you have a resume file named `fake_resume.md` in the root directory. You can use the provided one as a template and replace it with your own information in Markdown format.

---

## ▶️ How to Run

1.  **Launch Jupyter Notebook:**
    ```bash
    jupyter notebook
    ```

2.  **Open the Notebook:**
    In your browser, open the `L7_job_application_crew.ipynb` file.

3.  **Customize the Inputs:**
    Find the `job_application_inputs` dictionary cell and replace the placeholder values with the actual job posting you are targeting, your GitHub URL, and your personal write-up.

    ```python
    job_application_inputs = {
        'job_posting_url': '[https://example-job-posting-url.com](https://example-job-posting-url.com)',
        'github_url': '[https://github.com/your-github-username](https://github.com/your-github-username)',
        'personal_writeup': """Your concise professional summary here."""
    }
    ```

4.  **Execute the Crew:**
    Run all the cells in the notebook. The final cell, `job_application_crew.kickoff(...)`, will start the process. It may take several minutes to complete as the agents perform their tasks.

---

## 📈 Example Outputs

After execution, two new files will be created in your directory.

### 1. Tailored Resume (`tailored_resume.md`)

This file will contain the revised version of your resume, optimized for the job posting.

> ```markdown
> # Rishwanth J  
>
> 📞 7305656635 | 📧 rishwanth738@gmail.com  
> 🔗 [LinkedIn](...) | [GitHub](...)  
>
> ---
>
> ## 📌 Professional Summary  
> Highly motivated Computer Science student with a strong foundation in data structures, algorithms, machine learning, and software design. Proficient in Python, C++, and JavaScript, with hands-on experience developing AI-powered solutions and scalable backend systems. Skilled in building production-grade tools, fine-tuning language models, and working across Linux-based environments...
>
> *(...content will be tailored by the agent...)*
> ```

### 2. Interview Prep Materials (`interview_materials.md`)

This file will contain strategic questions and talking points to help you prepare for the interview.

> ### Interview Questions and Talking Points for Data Science Intern Position:
>
> 1.  **Technical Skills Assessment:**
>     -   Discuss your experience with Python and how you have used libraries like Pandas, NumPy, and Scikit-learn in your projects.
>     -   Can you explain a project where you applied machine learning techniques such as regularization, boosting, random forests, ensemble methods, or time series modeling?
>     -   Share details about your exposure to LLMs and Generative AI. How have you implemented these concepts in your projects?
>
> 2.  **Project Experience:**
>     -   Walk us through the SmartLogiX project. How did you achieve a 24% reduction in operational costs, and how did you integrate open-source APIs for efficiency?
>
> *(...more questions and talking points will be generated...)*
>
