## 🔬 Applying SDD to Scientific Data Analysis

For scientists and researchers who may not have a formal software engineering background, the SDD methodology can be adapted to bring structure and reproducibility to data analysis projects. It aligns well with the scientific method and helps manage complexity, even when using low-code tools or writing simple scripts.

### Adapting the SDD Phases for Data Analysis:

1.  **🧭 Steering Architect Mode: Frame the Research**
    -   **Product Vision** becomes the **Research Goal**. Clearly state your hypothesis or research question.
    -   **Tech Stack** becomes the **Analytical Toolkit**. Specify the datasets, software (e.g., Python with pandas, R, SPSS, Excel), and statistical methods you plan to use.
    -   **Artifacts**: Use the standard SDD artifact names, but adapt their content for the research context:
        -   `.ai-rules/product.md` (as **Research Goal**): Document the hypothesis, objectives, and expected outcomes.
        -   `.ai-rules/tech.md` (as **Analytical Toolkit**): List the data sources, software (e.g., Python, R), and key libraries/packages.

2.  **🗂️ Planning Mode: Design the Analysis Plan**
    -   **Requirements** become **Analysis Steps**. Break down the entire analysis into a sequence of clear, logical steps.
    -   **Design** focuses on the **Data Flow and Methodology**. Detail how data will be cleaned, transformed, what statistical models will be applied, and what visualizations will be created.
    -   **Tasks**: Following the standard SDD structure, create a dedicated folder for the analysis (e.g., `specs/exploratory-analysis/`). Inside, create a `tasks.md` file listing each step as a checkbox item. For example:
        -   `[ ] Load the dataset from source X.`
        -   `[ ] Clean the data (e.g., handle missing values, remove outliers).`
        -   `[ ] Perform exploratory data analysis (EDA).`
        -   `[ ] Apply statistical test Y.`
        -   `[ ] Generate plot Z to visualize the results.`

3.  **⚡ Execution Mode: Execute and Document**
    -   Follow the `tasks.md` list sequentially.
    -   Execute each step using your chosen tool (e.g., running a script, using a GUI).
    -   **Verification** involves checking the output of each step. For instance, after cleaning data, verify the dataset's dimensions and summary statistics. After running a model, check the output for correctness.
    -   **Log Results**: Document the results, figures, and interpretations from each step in the standard development log (e.g., `./dev-log/<yyyymmdd>.md`). This creates a traceable, chronological record of your analysis, making it transparent and reproducible.

By applying SDD, scientists can transform a conventional, often ad-hoc, analysis workflow into a systematic and well-documented process, greatly enhancing the reliability and clarity of their research.