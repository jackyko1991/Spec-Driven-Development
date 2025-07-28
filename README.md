# 🌟 Spec-Driven Development (SDD) Workflow

This document outlines the **Specification-Driven Development (SDD)** workflow, a structured approach for building software with agentic development tools like Claude Code, AWS Kiro, and Roo Code. SDD divides the development process into three distinct phases: **Steering Architect**, **Planning**, and **Execution**. This separation of concerns promotes rapid, high-quality code generation with enhanced clarity, maintainability, and traceability.

---

## 🚀 SDD Workflow Overview

The SDD workflow consists of three sequential phases:

1.  **🧭 Steering Architect Mode**: Define the project's high-level rules, product vision, technology stack, and overall structure.
2.  **🗂️ Planning Mode**: Collaboratively create detailed feature specifications, including requirements, design documents, and actionable tasks.
3.  **⚡ Execution Mode**: Implement the defined tasks atomically, verify their correctness, and incrementally update the codebase.

Each phase is supported by specialized agentic tools and context files, which enforce discipline and minimize ambiguity throughout the development lifecycle.

---

## 1. 🧭 Steering Architect Mode

**Responsibilities:**
- Analyze the existing codebase (if any) to establish a baseline.
- Generate or update foundational rule files (e.g., in an `.ai-rules/` directory).
- Document the product vision, technology stack, folder structure, and project-level architectural rules.

**Artifacts:**
- `.ai-rules/product.md`: Describes the product's purpose, features, and target audience.
- `.ai-rules/tech.md`: Specifies the programming languages, frameworks, and libraries to be used.
- `.ai-rules/structure.md`: Defines the project's directory layout and file organization.

---

## 2. 🗂️ Planning Mode

**Steps:**
- **Define Requirements**: Elicit and document requirements using methods like user stories, scenarios, or EARS (Event-Action-Response-State).
- **Design Solution**: Create high-level designs for modules, APIs, and interaction sequences.
- **Break Down Tasks**: Decompose the design into small, manageable tasks and analyze their dependencies.

**Spec Folder Structure:**
A dedicated folder is created for each feature to hold its specifications:
```text
specs/
  └── feature-name/
      ├── requirements.md
      ├── design.md
      └── tasks.md
```

**Collaborative Refinement:**
Engage in a dialogue with the AI agent to refine and clarify ideas. The agent should ask targeted questions (typically 3-5 per feature) to move from broad concepts to precise specifications, ensuring the resulting spec files are comprehensive and clear.

---

## 3. ⚡ Execution Mode

In Execution Mode, the agent functions as a focused coding assistant. It systematically reads the `tasks.md` file and generates incremental code changes with a strong emphasis on **Test-Driven Development (TDD)** to ensure functionality and reliability. The agent adheres to agile DevOps practices, delivering small, verifiable improvements that align with project requirements and maintain high code quality.

### Detailed Workflow:
1.  **Identify Task**: Open `tasks.md` and select the first unchecked (`[ ]`) task.
2.  **Understand Task**: Read the task description and refer to the corresponding `design.md` and `requirements.md` for full context.
3.  **Implement**: Apply a single, atomic code change to address only the current task.
4.  **Verify**: Follow the acceptance criteria or testing instructions defined in the task.
5.  **Reflect**: Document any project-wide learnings or newly established patterns in the "Rules & Tips" to ensure consistency.
6.  **Update State**:
    - If an automated test passes, mark the task as complete: `[x]`.
    - If verification is manual or no test exists, summarize the changes and ask the user to confirm functionality (unless running in autonomous mode). Upon confirmation, mark the task as `[x]`.
    - Summarize all changes in a development log, such as `./dev-log/<yyyymmdd>.md`.

### Parallel Feature Development:
Features can be developed in parallel, while tasks within each feature are executed sequentially. This enables efficient collaboration and faster delivery. For more on asynchronous local coding workflows, see [Asynchronous Coding on Local with Git Worktree](https://gist.github.com/jackyko1991/deb71662444b021c28f38e22c40be53d).

---

## 4. 🤖 Setting up the SDD Agents

This section provides instructions for configuring agentic tools like Claude Code and Roo Code to use the SDD methodology with sub-agents or modes.

### Agent Prompts
The prompts for each mode are essential for guiding the AI.
- [Steering Architect Mode Prompt](steering-architect-prompt.md)
- [Planning Mode Prompt](planning-mode-prompt.md)
- [Execution Mode Prompt](execution-mode-prompt.md)

### Claude Code Setup
1.  Use the `/agents` command in Claude Code and select `Create new agent`.
2.  Choose `Personal (~/.claude/agents/)` for global use or `Project (.claude/agents)` for project-specific use.
3.  Select `Manual configuration`.
4.  Set the Agent type (identifier) to `steering-architect`, `planning-mode`, or `execution-mode`.
5.  Copy the corresponding system prompt from the links above.
6.  Copy the description for the sub-agent from the prompt file's header.
7.  Allow the agent to use `All tools`.
8.  Set a color for the agent or leave it as automatic.
9.  Save the new agent.
10. Use the agent with a prompt like: `Use @steering-architect to create project guidance for a Python library.`

### Roo Code Setup
1.  Go to `Modes` -> `Mode Settings` -> `Create New Mode`.
2.  Provide a mode name, such as `🧭 Steering Architect`, `🗂️ Planning`, or `⚡ Execution`.
3.  Choose `Global` for the save location or `Project-specific` for local use.
4.  For `Role Definition`, copy the corresponding prompts from the links above.
5.  For `Short description (for humans)`, copy the description from the header of the prompt files.
6.  Leave `When to Use`, `Available Tools`, and `Custom Instructions` unchanged.
7.  Save the new mode.
8.  Switch to the corresponding mode and use a prompt like: `Create project guidance for a Python library project.`

---

## ✅ Best Practices for SDD

1.  **Maintain Separation of Concerns**: Strictly adhere to the responsibilities of each phase.
2.  **Create Atomic Tasks**: Ensure tasks are small, self-contained, and testable.
3.  **Use Context Files**: Always reference spec files for every change to maintain alignment.
4.  **Include Verification Steps**: Every task should have clear acceptance criteria.
5.  **Iterate on Specs**: Refine specifications based on learnings from implementation.
6.  **Keep Documentation Current**: Regularly update rules and documentation to reflect project evolution.


---

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

---

## Conclusion

This streamlined tutorial provides a robust framework for structured, traceable, and maintainable software development. By leveraging agentic tools within the SDD methodology, teams can build complex systems with greater speed, discipline, and quality.

## References
- [Kiro and the future of AI spec-driven software development](https://kiro.dev/blog/kiro-and-the-future-of-software-development/)
- [Claude Code Sub Agents](https://docs.anthropic.com/en/docs/claude-code/sub-agents)
- https://www.aivi.fyi/aiagents/introduce-Sub-agents