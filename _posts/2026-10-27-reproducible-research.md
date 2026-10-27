---
layout: post
title: Getting Started with GitHub for Reproducible Research
date: 2026-10-27 09:00:00+0100
description: A practical introduction to Git, GitHub, and reproducible research workflows for engineering students.
tags: git github version-control reproducibility research-tools
categories: tutorials
related_posts: false
giscus_comments: true
published: true
author: Ian He
---

Engineering research frequently involves developing models, writing simulation code, processing data, and comparing multiple design choices. As a project grows, it can become difficult to answer simple questions: **Which version produced this figure? What changed since the last simulation? Can someone else reproduce the result?**

**Git** and **GitHub** can help. Git tracks changes to files over time; GitHub hosts repositories online and supports collaboration, code review, and sharing. Used alongside good documentation and environment management, they form an important part of a reproducible research workflow.

This beginner-friendly guide introduces a workflow suitable for EASy PhD and MEng researchers working with Python, MATLAB, numerical simulations, and engineering models.

## 1. Why use GitHub in research?

Version control helps you:

- **Track changes:** Know when and why a model, script, or parameter was modified.
- **Recover previous versions:** Compare results or return to an earlier implementation.
- **Collaborate:** Review changes before integrating them into a shared project.
- **Connect results to code:** Record the version of code used for an experiment or figure.
- **Share research:** Make methods easier to inspect, reuse, and cite when publication permissions allow.

> GitHub is not a substitute for robust data storage, laboratory records, or validation. Reproducibility requires code, inputs, software dependencies, configuration, and instructions to be documented together.

## 2. Getting started: a simple workflow

Install [Git](https://git-scm.com/) and create a free account at [GitHub](https://github.com/). You can run the following commands in a terminal, including the integrated terminal in [Visual Studio Code](https://code.visualstudio.com/).

### Step 1: Clone a repository

Open a repository on GitHub and copy its HTTPS URL. For example, an EASy research repository can be cloned with:

```bash
git clone https://github.com/easy-research-lab/smpp-car-following.git
cd smpp-car-following
```

Cloning creates a local copy, including its version history. If you are using another project, replace the URL and directory name accordingly.

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

If you are preparing an environment specification from an existing Conda environment, a portable starting point is:

```bash
conda export --from-history --format=environment-yaml > environment.yml
```

Review the exported file before sharing it. A portable environment file helps others install the intended packages, but it does not guarantee identical versions on every platform. For stricter reproduction, record tested dependency versions and consider a lockfile or container.

For **MATLAB** projects, document the MATLAB release and required toolboxes. For **simulation software**, also record the solver version, model settings, input files, and computational platform where relevant.

## 4. Organise a research repository clearly

A straightforward research repository might use the following structure:

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

This is an **illustrative structure**, not a description of an existing EASy repository.

The `README.md` should tell readers what the research does, what they need to install, how to run a minimal example, what outputs to expect, and which publication to cite. Where possible, include a small demonstration dataset and a baseline result that users can reproduce.

Use a `.gitignore` file to exclude temporary files, local environments, and generated outputs that do not belong in version control. For example:

```gitignore
__pycache__/
*.pyc
.venv/
.ipynb_checkpoints/
```

**Do not commit** passwords, API tokens, private participant data, confidential industrial datasets, or unpublished information that you are not authorised to share. Git history can retain sensitive material even after a file is deleted.

## 5. Link simulations and publications to a specific code version

Imagine you are comparing two controllers for an electric vehicle. To make the study easier to reproduce, record:

1. The Git commit identifier used to generate the reported results (`git rev-parse HEAD`).
2. The model parameters, driving cycle, and data preprocessing steps.
3. The software environment and solver settings.
4. Any random seeds and details of repeated runs.
5. Instructions to generate the key figures and tables.

For a manuscript or thesis, document which code version produced each important result. If a repository is released publicly, a tagged version or archived release can provide a stable reference; the repository URL alone may change as new code is added.

## 6. Good habits for EASy researchers

- Commit small, meaningful changes regularly.
- Use descriptive branch and commit names.
- Keep source code separate from large raw datasets and temporary outputs.
- Include clear instructions for at least one reproducible example.
- Review your code and results before merging changes.
- Discuss with your supervisor what can be made public, especially for collaborative or industry-funded projects.
- Treat version control as part of research quality, not just software housekeeping.

## 7. Useful resources

- [GitHub Docs: About Git](https://docs.github.com/en/get-started/using-git/about-git)
- [GitHub Docs: Contributing to a project](https://docs.github.com/en/get-started/exploring-projects-on-github/contributing-to-a-project)
- [GitHub Docs: Ignoring files](https://docs.github.com/en/get-started/git-basics/ignoring-files)
- [Conda: Managing environments](https://docs.conda.io/projects/conda/en/stable/user-guide/tasks/manage-environments.html)
- [EASy Research Group on GitHub](https://github.com/easy-research-lab)

## Final thoughts

**Reproducible engineering research starts with being able to explain exactly how a result was produced.** Git and GitHub make it easier to track code development and collaborate; documented environments, inputs, and validation make the results scientifically useful. Starting these practices early can save considerable time when writing papers, completing a PhD thesis, or transferring a project to another researcher.