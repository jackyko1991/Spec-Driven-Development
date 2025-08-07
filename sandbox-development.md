# Sandbox Development Guide

[繁體中文](sandbox-development.zh-Hant.md)

This guide details the different sandboxing strategies that can be used in this development environment. Sandboxing is a critical practice for ensuring that new features, bug fixes, and experiments are developed in an isolated environment without affecting the stability of the main codebase.

## Strategy Comparison

| Strategy | Best For | Overhead | Isolation | Key Characteristic |
| :--- | :--- | :--- | :--- | :--- |
| **Git Checkout** | Most development tasks | Low | High | Uses a temporary branch for all changes. |
| **Directory Copy** | Small, isolated experiments | Medium | High | Creates a minimal copy of necessary files. |
| **Git Worktree** | Complex parallel development | High | Very High | Allows multiple branches to be checked out at once. |

## Unified Sandbox Location

All sandboxing methods utilize a unified `.sandbox/` directory at the root of the project for any file-based operations. This directory is ignored by Git (via `.gitignore`) to prevent temporary development artifacts from being committed to the repository.

## Sandboxing Strategies

### 1. Git Checkout

*   **Description:** This is a lightweight and highly recommended approach that leverages Git's branching capabilities. A new temporary branch is created from the current base branch for each task. All changes are committed to this branch, keeping the main branch clean.
*   **Best for:** Most development tasks, including new features and bug fixes. It provides excellent isolation with minimal overhead.
*   **Workflow:**
    1.  A new branch (e.g., `feature/user-auth` or `fix/login-bug`) is created.
    2.  All development and commits occur on this branch.
    3.  Once the work is complete and verified, the branch is merged back into the main development branch.

### 2. Directory Copy

*   **Description:** This method involves creating a minimal copy of only the necessary files for a specific task into a subdirectory within `.sandbox/`. This is a simple way to achieve isolation without relying on Git features.
*   **Best for:** Small, isolated experiments or when you need to work with a subset of the project without the overhead of the full application.
*   **Workflow:**
    1.  A new directory is created (e.g., `.sandbox/2023-10-27-test-new-algorithm/`).
    2.  Only the files required for the task are copied into this directory.
    3.  Changes are made in the isolated directory.
    4.  Once complete, the modified files are manually copied back to the main project.

### 3. Git Worktree

*   **Description:** This is an advanced Git feature that allows you to have multiple working trees attached to the same repository. This means you can have multiple branches checked out simultaneously in different directories.
*   **Best for:** Complex scenarios requiring parallel development on multiple features or long-running branches. It avoids the need to switch branches in your primary development directory.
*   **Workflow:**
    1.  A new worktree is created and linked to a new or existing branch.
    2.  The worktree is created in a new directory, often within `.sandbox/`.
    3.  Development occurs in the isolated worktree.
    4.  Changes are committed and can be merged as usual.

## Choosing a Strategy

The `steering-architect` and `strategic-planner` agents will guide you in selecting the appropriate strategy for your task. The `git checkout` method is the default recommendation for most cases due to its balance of power and simplicity.