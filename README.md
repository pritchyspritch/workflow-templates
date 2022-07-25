# workflow-templates

This repository contains template GitHub Actions workflow files that consume the [Reusable Workflows](https://github.com/pritchyspritch/reusable-workflows).

## Templates

You can find the template workflows in the [templates folder](templates/). The templates supplied here include the:

* [Static analysis code scanning template](templates/consumed-codeql-workflow.yml)
* [Static analysis extended security code scanning template](templates/consumed-extended-sec-codeql-workflow.yml)
* [Static analysis security and quality code scanning template](templates/consumed-sec-and-quality-codeql-workflow.yml)
* [Container scanning template](templates/consumed-container-workflow.yml)
* [Terraform scanning template](templates/consumed-tfsec-workflow.yml)
* [Vulnerability scanning template](templates/consumed-nuclei-workflow.yml)

## Template descriptions

### Static Analysis Code Scanning Templates
These templates implement the CodeQL static analysis scanning reusable workflows. The language used in your repo must be added to the template files, the default in the files are C#.

For the default rules, you can reference `reusable-codeql-workflow.yml@main`:
```
[...]
    uses: pritchyspritch/reusable-workflows/.github/workflows/reusable-codeql-workflow.yml@main
    with:
      language: 'csharp'
```

For extended security rules, you can reference `reusable-extended-sec-codeql.yml`:
```
[...]
    uses: pritchyspritch/reusable-workflows/.github/workflows/reusable-extended-sec-codeql.yml@main
    with:
      language: 'csharp'
```

For security and code quality rules, you can reference `reusable-sec-and-quality-codeql.yml`:
```
[...]
    uses: pritchyspritch/reusable-workflows/.github/workflows/reusable-sec-and-quality-codeql.yml@main
    with:
      language: 'csharp'
```

### Container Scanning Template
This template implements the container scanning reusable workflow. The Dockerfile path must be added to the template file:

```
[...]
    uses: pritchyspritch/reusable-workflows/.github/workflows/reusable-container-workflow.yml@main
    with:
      docker-path: './Docker-test'
```

### Terraform Scanning Template
This template implements the terraform scanning reusable workflow. The terraform directory path must be added to the template file:

```
[...]
    uses: pritchyspritch/reusable-workflows/.github/workflows/reusable-tfsec-workflow.yml@main
    with:
      terraform-path: 'terraform/aws' 
```

### Vulnerability Scanning Template
This template implements the vulnerability scanning reusable workflow. The template has example workflow calls based on a build workflow running successfully due to the assumption that a vulnerability scan will run once the changes are deployed:

```
on:
  workflow_run:
    workflows: [Build] # A workflow has run to build a web application / component and has completed
    types: [completed]
[...]
```

The web application URL must be added to the template file:
```
[...]
      uses: pritchyspritch/reusable-workflows/.github/workflows/reusable-vulnerabilityscan-workflow.yml@main
      with:
        website-url: 'https://pritchyspritch.github.io' # Set website URL
```
