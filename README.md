# Azure-Pipeline-Automatic-Trigger
Here's a complete overview of **Azure Pipeline automatic triggers** along with **YAML code examples** to help you configure continuous integration (CI) and continuous deployment (CD) scenarios.

---

### ✅ **1. Continuous Integration (CI) Trigger**

Runs pipeline automatically when code is pushed to a branch (e.g., `main`).

```yaml
trigger:
  branches:
    include:
      - main
```

You can also exclude branches:

```yaml
trigger:
  branches:
    exclude:
      - dev
```

---

### ✅ **2. Path Filters in Trigger**

Only trigger when specific paths change.

```yaml
trigger:
  branches:
    include:
      - main
  paths:
    include:
      - src/*
    exclude:
      - docs/*
```

---

### ✅ **3. Continuous Deployment (CD) with Pull Request (PR) Trigger**

Triggers pipeline when a PR is created targeting `main`.

```yaml
pr:
  branches:
    include:
      - main
```

---

### ✅ **4. Scheduled Trigger**

Run pipeline on a schedule (e.g., nightly build).

```yaml
schedules:
  - cron: "0 2 * * *" # At 2 AM daily
    displayName: Nightly Build
    branches:
      include:
        - main
    always: true
```

> 📌 `cron` uses UTC time.

---

### ✅ **5. Pipeline Resource Trigger**

Trigger pipeline when another pipeline completes.

```yaml
resources:
  pipelines:
    - pipeline: upstreamPipeline
      source: my-upstream-pipeline
      trigger: true
```

---

### ✅ **6. Full Sample YAML for CI/CD**

```yaml
trigger:
  branches:
    include:
      - main

pr:
  branches:
    include:
      - main

pool:
  vmImage: ubuntu-latest

steps:
  - task: NodeTool@0
    inputs:
      versionSpec: '16.x'
    displayName: 'Install Node.js'

  - script: |
      npm install
      npm run build
    displayName: 'Build Project'

  - task: PublishBuildArtifacts@1
    inputs:
      PathtoPublish: 'dist'
      ArtifactName: 'drop'
      publishLocation: 'Container'
```

---

Would you like a real GitHub example repo or a pipeline for .NET, Python, or another tech stack?
