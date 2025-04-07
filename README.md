# Auto Job Applier for LinkedIn

An automated tool that helps you apply to jobs on LinkedIn with customizable search criteria and application responses.

## Table of Contents
- [Auto Job Applier for LinkedIn](#auto-job-applier-for-linkedin)
  - [Table of Contents](#table-of-contents)
  - [Installation](#installation)
    - [Windows](#windows)
      - [ChromeDriver](#chromedriver)
      - [UV setup](#uv-setup)
    - [Linux/Mac](#linuxmac)
  - [Configuration](#configuration)
    - [Secrets Configuration](#secrets-configuration)
    - [Personal Information](#personal-information)
    - [Job Application Questions](#job-application-questions)
    - [Search Preferences](#search-preferences)
    - [General Settings](#general-settings)
    - [Environment Setup](#environment-setup)
  - [Usage](#usage)
  - [Resume Setup](#resume-setup)
  - [Troubleshooting](#troubleshooting)

## Installation

### Windows

#### ChromeDriver

To set up the project on Windows:

1. Navigate to the setup directory:
   ```
   cd setup
   ```

2. Run the Windows setup script as administrator:
   ```
   .\windows-setup.bat
   ```
   
   You'll see a prompt:
   ```
   Please run this setup as admin.
   Requesting administrative privileges...
   ```
   
   The script will automatically request administrative privileges if needed.

3. Follow any additional prompts to complete the installation.

The setup script will install all necessary dependencies and configure your environment for the Auto Job Applier for LinkedIn.


#### UV setup

1. Open PowerShell as Administrator and run:
   ```powershell
   powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
   ```

2. Add UV to your PATH:
   ```powershell
   [Environment]::SetEnvironmentVariable("Path", $env:Path + ";C:\Users\$env:USERNAME\.local\bin", "User")
   ```
   This adds UV to your PATH using your Windows username automatically.

3. Create a virtual environment and install dependencies:
   ```powershell
   C:\Users\%USERNAME%\.local\bin\uv.exe venv
   ```

4. Activate the virtual environment:
   ```powershell
   .\.venv\Scripts\activate
   C:\Users\%USERNAME%\.local\bin\uv.exe pip install -r .\requirements.txt
   ```

5. Run the bot:
   ```powershell
   python .\runAiBot.py
   ```

### Linux/Mac

1. Install UV:
   ```bash
   curl -LsSf https://astral.sh/uv/install.sh | sh
   ```
   
   For custom installation path:
   ```bash
   curl -LsSf https://astral.sh/uv/install.sh | env UV_INSTALL_DIR="/custom/path" sh
   ```

2. Create a virtual environment and install dependencies:
   ```bash
   uv venv
   uv pip install -r requirements.txt
   ```

3. Activate the virtual environment:
   ```bash
   source ./venv/bin/activate
   ```

4. Run the bot:
   ```bash
   python runAiBot.py
   ```

## Configuration

Before running the bot, you need to configure several files in the `config` directory:

### Secrets Configuration
File: `config/secrets.py`

- **AI Configuration** (Optional):
  ```python
  use_AI = True  # Set to False if you don't want to use AI
  llm_api_url = "http://localhost:11434/v1/"  # Local LLM or OpenAI API URL
  llm_model = "model_name"  # Model name (e.g., "deepseek-r1:8b", "gpt-3.5-turbo")
  llm_spec = "openai-like"  # API specification
  stream_output = False  # Stream AI output
  ```

### Personal Information
File: `config/personals.py`

- **Basic Information**:
  ```python
  first_name = "Your First Name"
  middle_name = "Your Middle Name"  # Optional
  last_name = "Your Last Name"
  phone_number = "1234567890"  # 10-digit number
  current_city = "Your City"  # Leave empty to use job location
  ```

- **Equal Opportunity Information** (Optional):
  ```python
  ethnicity = "Asian"  # Options: "Decline", "Hispanic/Latino", "American Indian or Alaska Native", "Asian", "Black or African American", "Native Hawaiian or Other Pacific Islander", "White", "Other"
  gender = "Male"  # Options: "Male", "Female", "Other", "Decline"
  disability_status = "No"  # Options: "Yes", "No", "Decline"
  veteran_status = "No"  # Options: "Yes", "No", "Decline"
  ```

### Job Application Questions
File: `config/questions.py`

- **Resume and Profile**:
  ```python
  default_resume_path = "path/to/your/resume.pdf"  # Relative or absolute path
  linkedin_headline = "Your LinkedIn Headline"
  linkedin_summary = "Your LinkedIn Summary"
  years_of_experience = "2"  # Number in quotes
  ```

- **Application Details**:
  ```python
  require_visa = "No"  # "Yes" or "No"
  website = "https://your-website.com"  # Your portfolio website
  linkedIn = "https://www.linkedin.com/in/your-profile"  # Your LinkedIn profile
  us_citizenship = "Other"  # Citizenship status
  ```

- **Salary and Employment**:
  ```python
  desired_salary = 100000  # Expected salary (number without quotes)
  current_ctc = 80000  # Current salary (number without quotes)
  notice_period = 30  # Notice period in days
  recent_employer = "Your Current Employer"
  ```

- **Application Control**:
  ```python
  pause_before_submit = True  # Pause before submitting application
  pause_at_failed_question = True  # Pause if bot can't answer a question
  overwrite_previous_answers = False  # Overwrite previous answers
  ```

### Search Preferences
File: `config/search.py`

- **Search Terms**:
  ```python
  search_terms = [
      "Software Engineer",
      "Data Scientist",
      "Machine Learning Engineer",
      # Add more job titles
  ]
  ```

- **Location and Search Control**:
  ```python
  search_location = "Your Location"  # e.g., "United States", "India"
  switch_number = 30  # Number of applications before switching search
  randomize_search_order = False  # Randomize search order
  ```

- **Job Filters**:
  ```python
  sort_by = "Most recent"  # "Most recent", "Most relevant"
  date_posted = "Past week"  # "Any time", "Past month", "Past week", "Past 24 hours"
  salary = "$100,000+"  # Salary filter
  easy_apply_only = True  # Only show Easy Apply jobs
  
  # Multiple select filters
  experience_level = ["Entry level", "Associate", "Mid-Senior level"]
  job_type = ["Full-time"]
  on_site = ["On-site", "Remote", "Hybrid"]
  
  # Company and industry filters
  companies = []  # List of specific companies
  industry = ["Information Technology", "Software Development"]
  job_function = ["Engineering", "Information Technology"]
  ```

- **Skip Filters**:
  ```python
  about_company_bad_words = ["Staffing", "Recruiting"]  # Skip companies with these words
  bad_words = []  # Skip jobs with these words in description
  current_experience = 3  # Your current experience level
  ```

### General Settings
File: `config/settings.py`

- **LinkedIn Behavior**:
  ```python
  close_tabs = True  # Close external application tabs
  follow_companies = True  # Follow companies after applying
  run_non_stop = True  # Run continuously
  ```

- **File Paths**:
  ```python
  generated_resume_path = "all resumes/"  # Path for generated resumes
  file_name = "all excels/all_applied_applications_history.csv"  # History file
  failed_file_name = "all excels/all_failed_applications_history.csv"  # Failed applications
  logs_folder_path = "logs/"  # Logs directory
  ```

- **Browser Settings**:
  ```python
  click_gap = 0  # Wait time between clicks
  run_in_background = False  # Run Chrome in background
  disable_extensions = False  # Disable Chrome extensions
  safe_mode = True  # Run in safe mode
  smooth_scroll = False  # Enable smooth scrolling
  keep_screen_awake = True  # Prevent PC from sleeping
  stealth_mode = False  # Run in undetected mode
  ```

### Environment Setup

1. Create a `.env` file in the root directory of the project with the following variables:

```
GEMINI_API_KEY=your_gemini_api_key
GOOGLE_API_KEY=your_google_api_key
LINKEDIN_EMAIL=your_linkedin_email
LINKEDIN_PASSWORD=your_linkedin_password
AI_API_KEY=ollama  # or your preferred AI service
```

**Important**: Never commit your `.env` file to version control. The `.gitignore` file should already exclude it.

## Usage

1. Make sure you have configured all the necessary files in the `config` directory.
2. Place your resume in the specified path (default: `all resumes/` directory).
3. Ensure the `all excels/` and `logs/` directories exist for storing application history and logs.
4. Run the bot:
   ```
   python runAiBot.py
   ```

## Resume Setup

1. Place your resume PDF file in the `all resumes/` directory.
2. Update the `default_resume_path` in `config/questions.py` to point to your resume file.
3. Make sure your resume is tailored to the job types you're applying for.

## Troubleshooting

- **Browser Issues**: If Chrome fails to open, try setting `safe_mode = True` in `config/settings.py`.
- **Application Failures**: Check the logs in the `logs/` directory for error details.
- **LinkedIn Detection**: If LinkedIn detects automation, try enabling `stealth_mode = True` in `config/settings.py`.
- **AI Integration Issues**: If using AI features, ensure your API keys and URLs are correct in `config/secrets.py`.


