# MyProject: Automated Data Processing and PublishingThis project demonstrates a robust workflow for processing data from an Excel file, ensuring code quality with linting, and automatically publishing the processed results using GitHub Actions and GitHub Pages.## Table of Contents- [Project Overview](#project-overview)- [Features](#features)- [Setup](#setup)- [Usage](#usage)- [Data Files](#data-files)- [CI/CD Workflow](#cicd-workflow)- [License](#license)## Project OverviewThe core of this project revolves around transforming an initial `data.xlsx` Excel file into a processed JSON output (`result.json`). This transformation is handled by a Python script (`execute.py`). To ensure consistency and reliability, a GitHub Actions workflow automates code quality checks (using Ruff), script execution, and the publishing of the final `result.json` to GitHub Pages.## Features- **Excel to CSV Conversion**: `data.xlsx` is first converted to `data.csv` for standardized processing. `data.csv` is committed to the repository.- **Python Data Processing**: `execute.py` reads `data.csv`, performs necessary data manipulations, and generates `result.json`.- **Code Quality**: Integration of `Ruff` for linting Python code, ensuring adherence to best practices and identifying potential issues early.- **Automated Workflow**: A GitHub Actions CI/CD pipeline automates the entire process from code commit to result publishing.- **GitHub Pages Publication**: `result.json` is automatically published to GitHub Pages, making the latest processed data easily accessible.## SetupTo run this project locally, ensure you have Python 3.11+ installed.### Prerequisites- Python 3.11+- `pip` (Python package installer)### Installation1.  **Clone the repository**:
    ```bash
    git clone https://github.com/your-username/myproject.git
    cd myproject
    ```2.  **Create a virtual environment** (recommended):
    ```bash
    python -m venv venv
    source venv/bin/activate # On Windows: `venv\Scripts\activate`
    ```3.  **Install dependencies**:
    ```bash
    pip install pandas ruff openpyxl
    ```
    - `pandas`: For data manipulation and Excel/CSV handling.
    - `ruff`: For Python code linting.
    - `openpyxl`: Required by pandas to read `.xlsx` files.## Usage### Local Execution1.  **Ensure data files are present**: Make sure `data.xlsx` and `data.csv` are in the root directory.
2.  **Run the processing script**:
    ```bash
    python execute.py > result.json
    ```
    This will execute `execute.py` and direct its standard output to `result.json`.### Linting with RuffTo check code quality locally:
```bash
ruff check .
ruff format . --check # To check formatting, --diff to see changes
```## Data Files-   **`data.xlsx`**: The original input Excel file containing raw data.
-   **`data.csv`**: The CSV version of `data.xlsx`. This file is committed to the repository and is the primary input for `execute.py`.
-   **`execute.py`**: The Python script responsible for reading `data.csv`, processing it, and outputting `result.json`.
-   **`result.json`**: The final processed output in JSON format. This file is *not* committed to the repository but is generated and published via GitHub Actions.## CI/CD WorkflowThe project utilizes GitHub Actions for continuous integration and continuous deployment. The workflow is defined in `.github/workflows/ci.yml` and triggers on every push to the repository.The workflow performs the following steps:
1.  **Checkout Code**: Retrieves the repository content.
2.  **Set up Python**: Configures Python 3.11+.
3.  **Install Dependencies**: Installs `pandas`, `ruff`, and `openpyxl`.
4.  **Convert `data.xlsx` to `data.csv`**: Ensures `data.csv` is always up-to-date with `data.xlsx` within the CI environment.
5.  **Run Ruff Linting**: Executes `ruff check .` and `ruff format . --check` to enforce code style and identify errors.
6.  **Run Processing Script**: Executes `python execute.py > result.json` to generate the output.
7.  **Upload Artifacts**: Uploads `result.json` as a workflow artifact.
8.  **Deploy to GitHub Pages**: Uses `actions/upload-pages-artifact` and `actions/deploy-pages` to publish `result.json` to GitHub Pages. The `result.json` will be accessible at `https://your-username.github.io/your-repository-name/result.json`.## LicenseThis project is licensed under the MIT License - see the [LICENSE](#license) file for details.