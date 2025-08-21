[![DelivOps banner](https://raw.githubusercontent.com/delivops/.github/main/images/banner.png?raw=true)](https://delivops.com)

# Terraform GitHub Action

![Terraform](https://img.shields.io/badge/Terraform-FMT-purple)

**Fully automated Terraform formatting and commit GitHub Action.**

This GitHub Action automatically:
- Formats Terraform files using `terraform fmt`
- Commits and pushes any formatting changes to the branch that triggered the workflow

---

## How it works

This GitHub Action runs the following steps:

1. Checks out the code.
2. Configures Git to use the triggering GitHub user.
3. Installs Terraform (default version: `1.9.8`).
4. Runs `terraform fmt -recursive` to format all Terraform files.
5. If changes are detected, it auto-commits and pushes the updated files back to the same branch.

---

## Features

✔️ **Terraform Auto-formatting**  
Ensures Terraform code is consistently formatted according to best practices.

✔️ **Pushes Fixes Automatically**  
Fixes and commits formatting changes to the same branch — no manual intervention needed.

✔️ **Commits as GitHub Actor**  
Commits are authored using the GitHub username that triggered the action, preserving auditability.

---

## Inputs

| Name               | Description                                      | Required | Default   |
|--------------------|--------------------------------------------------|----------|-----------|
| `working_directory`| Directory containing Terraform configuration     | ✅       | —         |
| `terraform_version`| Terraform version to install                     | ❌       | `1.9.8`   |
| `github_token`     | GitHub token to authenticate and push commits    | ✅       | —         |

---

## 🚀 Usage

```yaml
name: Terraform Format

on:
  workflow_dispatch:

jobs:
  terraform-fmt:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Run Terraform Format
        uses: delivops/terraform-fmt-action@v0.0.1
        with:
          working_directory: "./"
          terraform_version: "1.9.8"
          github_token: ${{ secrets.GITHUB_TOKEN }}
