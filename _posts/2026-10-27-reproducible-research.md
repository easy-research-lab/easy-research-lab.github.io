---
layout: post
title: Getting Started with GitHub for Reproducible Research
date: 2026-10-27 09:00:00+0100
description: A practical introduction to Git, GitHub, and reproducible research workflows for engineering students.
tags: git reproducibility research-tools
categories: technical-tutorials 
related_posts: false
giscus_comments: true
published: true
author: Ian He
---

Engineering research frequently involves developing models, writing simulation code, analysing data, exploring design alternatives, preparing research papers in LaTeX or Overleaf, and maintaining technical documentation. As a project grows, it can become difficult to answer simple questions: **Which version produced this figure? What changed since the last simulation? Can someone else reproduce the result?**

**Git** and **GitHub** can help. Git tracks changes to files over time; GitHub hosts repositories online and supports collaboration, code review, and sharing. Used alongside good documentation and environment management, they form an important part of a reproducible research workflow.

## 1. Why use GitHub in research?

Version control helps you:

- **Track changes:** Know when and why a model, script, or parameter was modified.
- **Recover previous versions:** Compare results or return to an earlier implementation.
- **Collaborate:** Review changes before integrating them into a shared project.
- **Share research:** Make methods easier to inspect, reuse, and cite when publication permissions allow.

> GitHub is not a substitute for robust data storage, laboratory records, or validation. Reproducibility requires code, inputs, software dependencies, configuration, and instructions to be documented together.

## 2. Getting started: a simple workflow

Install [Git](https://git-scm.com/) and create a free account at [GitHub](https://github.com/). You can run the following commands in a terminal, including the integrated terminal in [Visual Studio Code](https://code.visualstudio.com/).

### Step 1: Clone a repository

Open a repository on GitHub and copy its HTTPS URL. For example, an EASy Lab research repository can be cloned with:

```bash
git clone https://github.com/easy-research-lab/smpp-car-following.git
cd smpp-car-following
```

Cloning creates a local copy, including its version history.

### Step 2: Create a branch

Make changes on a separate branch rather than directly on the main branch:

```bash
git switch -c improve-model-validation
```

A branch provides a place to test improvements without immediately altering the main version of the project.

### Step 3: Review and commit your changes

After editing a script or adding documentation:

```bash
git status
git diff
git add path/to/changed_script.py
git commit -m "Add validation plots for vehicle model"
```

Replace `path/to/changed_script.py` with an actual file you have changed. A **commit** records a snapshot of selected changes and a short explanation. Prefer informative messages such as `Fix battery SOC calculation` rather than `update` or `final version`.

### Step 4: Push and propose the changes

```bash
git push -u origin improve-model-validation
```

If you have permission to push to the repository, open GitHub and create a **pull request**. This allows supervisors and collaborators to review the changes before merging them. If you do not have write access, first fork the repository and push your branch to your fork.

Before starting a new task on an existing project, update your local branch using the team's agreed workflow (for example, `git pull` when on the correct tracking branch).

## 3. Make your computational environment reproducible

Two researchers may run the same script and obtain different results if they use different Python or library versions. Recording dependencies helps avoid this problem.

For Python projects, one option is a Conda environment. A simple `environment.yml` might look like this:

```yaml
name: engineering-research
channels:
  - conda-forge
dependencies:
  - python=3.11
  - numpy
  - scipy
  - matplotlib
  - pandas
```

After installing [Miniconda](https://www.anaconda.com/docs/getting-started/miniconda/main), create and activate the environment:

```bash
conda env create -f environment.yml
conda activate engineering-research
```

After installing or updating packages, export the environment specification:

```bash
conda env export > environment.yml
```

For **MATLAB** projects, document the MATLAB release and required toolboxes. For **simulation software**, also record the solver version, model settings, input files, and computational platform where relevant.

## 4. Organise a research repository clearly

A straightforward research repository might use the following example structure:

```text
my-research-project/
├── README.md
├── environment.yml
├── .gitignore
├── src/
│   └── model.py
├── examples/
│   └── run_example.py
├── configs/
│   └── baseline.yaml
├── tests/
│   └── test_model.py
└── results/
    └── README.md
```

The `README.md` should tell readers what the research does, what they need to install, how to run a minimal example, what outputs to expect, and which publication to cite. Where possible, include a small demonstration dataset and a baseline result that users can reproduce.

Use a `.gitignore` file to exclude temporary files, local environments, and generated outputs that do not belong in version control. For example:

```gitignore
__pycache__/
*.pyc
.venv/
.ipynb_checkpoints/
```

**Do not commit** passwords, API tokens, confidential datasets, or unpublished information that you are not authorised to share. Git history can retain sensitive material even after a file is deleted.

## 5. Good habits for EASy researchers

- Commit small, meaningful changes regularly.
- Use descriptive branch and commit names.
- Keep source code separate from large raw datasets and temporary outputs.
- Include clear instructions for at least one reproducible example.
- Review your code and results before merging changes.
- Discuss with your supervisor what can be made public, especially for collaborative projects.
- Treat version control as part of research quality, not just software housekeeping.

## 6. Useful resources

- [GitHub Docs: About Git](https://docs.github.com/en/get-started/using-git/about-git)
- [GitHub Docs: Contributing to a project](https://docs.github.com/en/get-started/exploring-projects-on-github/contributing-to-a-project)
- [GitHub Docs: Ignoring files](https://docs.github.com/en/get-started/git-basics/ignoring-files)
- [Conda: Managing environments](https://docs.conda.io/projects/conda/en/stable/user-guide/tasks/manage-environments.html)

<div class="mt-3">
  <div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden;">
    <iframe
      src="https://www.youtube.com/embed/S0kw9OB2Tf0?si=lacW7CnEjm09RfA3"
      title="Reproducible research - Version control with Git"
      style="position: absolute; top: 0; left: 10%; width: 80%; height: 100%;"
      frameborder="0"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
      referrerpolicy="strict-origin-when-cross-origin"
      allowfullscreen>
    </iframe>
  </div>
</div>

<div class="text-center">
    <em>Video. 1. Reproducible research and version control with Git.</em>
</div>
