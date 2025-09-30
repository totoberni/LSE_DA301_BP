# LSE DA301: Advanced Analytics - Turtle Games Project

This repository contains the coursework for the LSE Data Analytics Career Accelerator course DA301. The project involves a comprehensive analysis of the Turtle Games dataset to derive business insights on customer loyalty, segmentation, and sentiment. The analysis is conducted using both Python for machine learning tasks and R for statistical modeling and visualization.

-----

## Repository Structure

The project is organized into separate directories for data, Python notebooks, R scripts, and final reports. The R environment is managed by `renv` for full reproducibility.

```plaintext
LSE_DA301_BP/
├── Data/
│   ├── metadata_turtle_games.txt
│   ├── turtle_reviews.csv
│   └── turtle_reviews_2.csv
├── Python/
│   ├── .venv
│   ├── Berni_Alberto_DA301_Assignment_Notebook.ipynb
│   └── requirements.txt
├── R/
│   ├── Berni_Alberto_DA301_Assignment_Notebook.html
│   ├── Berni_Alberto_DA301_Assignment_Notebook.pdf
│   ├── Berni_Alberto_DA301_Assignment_Notebook.Rmd
│   ├── Berni_Alberto_DA301_Assignment_Script.R
│   ├── LSE_DA301_Assignment_R_template.R
│   └── out/
│       └── Turtle_Games_EDA_Report_temp.html
├── Reports/
├── renv/
│   ├── activate.R
│   └── settings.json
├── .Rprofile
├── .gitignore
├── renv.lock
└── README.md
```

-----

## Environment Setup

To ensure full reproducibility of the analysis, please follow the setup instructions below.

### R Environment

The R analysis uses the **`renv`** package to create a reproducible, project-specific environment.

1.  **Prerequisites**: Before you begin, ensure you have the necessary system-level software installed.
    
    **R**: You must have a base installation of R. You can download it from the [Comprehensive R Archive Network (CRAN)](https://cran.r-project.org/).
    
    **Pandoc**: The `rmarkdown` package, which is used to generate reports, requires **Pandoc** as a system dependency. RStudio typically bundles this automatically, but for standalone R setups (like in VS Code), it must be installed separately.
    
    **Download**: Go to the [official Pandoc installation page](https://pandoc.org/installing.html).
    
    * **Windows**: Download and run the `.msi` installer. The installer will automatically add Pandoc to your system's PATH, which is required.

    *   **macOS**: The recommended installation method is using [Homebrew](https://brew.sh/). In your terminal, run: 
    
        ```bash
        brew install pandoc
        ```
            
    *   **Linux**: Use your distribution's package manager. For example, on Debian/Ubuntu, run: 
    
        ```bash 
        sudo apt-get install pandoc
        ```
    
    **Verify Installation**: After installing, close and reopen your terminal or IDE, then run: 
    
    ```bash
    pandoc --version
    ```

    You should see the installed version number (`1.12.3 or higher`).

2.  **Clone the Repository**: If you haven't already, clone the project to your local machine.

    ```bash
    git clone <your-repository-url>
    cd LSE_DA301_BP
    ```

3.  **Open the Project in R**: Start an R session with the project's root directory as the working directory. The easiest way to do this is by opening the project in an IDE like RStudio or VS Code (with the R extension).

4.  **Restore the `renv` Environment**: When you first open the project, the `.Rprofile` script should automatically detect the lockfile. If prompted, agree to restore the environment from the lockfile. If you are not prompted, simply run the following command in the R console:

    ```r
    renv::activate()
    ```

    This command creates an `R Virtual Environment (renv)` and generates a `.Rprofile` reference that will start the `renv` when `.R` project files are open next.

    ```r
    renv::restore()
    ```

    This command reads the `renv.lock` file and installs the exact versions of all required R packages, ensuring a fully reproducible setup.\
    You are now ready to run the analysis in `R/Berni_Alberto_DA301_Assignment_Notebook.Rmd`.

-----

### Python Environment

The Python analysis is managed within a dedicated virtual environment.

1.  **Prerequisites: Install Build Tools**:
    Some Python packages, like `numpy`, may need to be compiled from source if a pre-compiled version (a "wheel") is not available for your Python version on Windows. This requires the Microsoft C++ Build Tools.
    -   Go to the [Visual Studio downloads page](https://visualstudio.microsoft.com/downloads/).
    -   Scroll down to **All downloads**, expand **Tools for Visual Studio**, and download the **Build Tools for Visual Studio**.
    -   Run the installer and select the **Desktop development with C++** workload.

2.  **Clone the repository** to your local machine:

    ```bash
    git clone <your-repository-url>
    cd LSE_DA301_BP
    ```

3.  **Navigate to the Python directory**:

    ```bash
    cd Python
    ```

4.  **Create a virtual environment**:

    ```bash
    python3.12 -m venv .venv
    ```
> `Compatibility note:` We must specify the Python version number because some packages are not available in the latest Python version `3.13.7`
5.  **Activate the environment**:

      * On **macOS/Linux**:
        ```bash
        source .venv/bin/activate
        ```
      * On **Windows**:
        ```powershell
        .\.venv\Scripts\activate
        ```

6.  **Install the required dependencies**: With the environment activated, install all necessary libraries from the `requirements.txt` file.

    ```bash
    pip install -r requirements.txt
    ```

7.  **Register the environment as a Jupyter Kernel**: This step makes your virtual environment available within Jupyter, ensuring your notebook uses the correct packages.

    ```bash
    python -m ipykernel install --user --name=lse-da301-project
    ```

8.  **Launch Jupyter and Run the Notebook**:

      * From terminal:
        ```bash
        jupyter notebook
        ```
      * From your IDE (VS Code):
        Open `Berni_Alberto_DA301_Assignment_Notebook.ipynb` from your IDE.  
        Go to `Kernels > Change Kernel`  
        Select `Jupyter Kernel` and select **`lse-da301-project`**.