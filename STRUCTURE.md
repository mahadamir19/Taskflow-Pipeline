<div align="center">

# TaskFlow Cloud Pipeline

### Cloud Development

<img alt="Azure" src="https://img.shields.io/badge/Azure-App%20Service%20%7C%20Functions%20%7C%20AKS%20%7C%20ACI-7c3aed?style=for-the-badge">

</div>

**GitHub repository description:** Starter repository for CS487 PA4, an Azure TaskFlow pipeline using App Service, Durable Functions, AKS, ACI, Blob Storage, and ACR.

<div style="background:#f5f3ff;color:#111827;border-left:6px solid #7c3aed;padding:14px 18px;border-radius:10px;margin:18px 0;">
This repository is the required starter structure for PA4. Fork it, complete the TODOs, deploy the Azure resources, commit your screenshots and write-up, then submit only your GitHub repository URL to the LMS.
</div>

## Architecture

```text
User Browser
    |
    v
App Service Web App
    |
    v
Azure Durable Function Orchestrator
    |-- calls --> AKS validate-api service
    |
    |-- creates --> Azure Container Instance report-job
                         |
                         v
                    Blob Storage PDF

All container images are stored in Azure Container Registry.
```

## Project Structure

```text
pa4-starter/
|-- webapp/                # Node.js / Express dashboard and proxy
|   |-- server.js
|   |-- public/
|   |   |-- index.html
|   |   +-- Cloud fr.avif
|   +-- package.json
|-- function-app/          # Azure Durable Function container
|   |-- function_app.py    # TODO: complete orchestrator and activities
|   |-- Dockerfile
|   |-- host.json
|   |-- local.settings.json
|   +-- requirements.txt
|-- validate-api/          # FastAPI validator deployed to AKS
|   |-- app.py
|   |-- Dockerfile
|   |-- requirements.txt
|   +-- k8s/
|       |-- deployment.yaml
|       +-- service.yaml
|-- report-job/            # One-shot PDF generator for ACI
|   |-- generate.py
|   |-- Dockerfile
|   +-- requirements.txt
|-- docs/                  # Put all screenshots and architecture diagram here
|-- SUBMISSION_TEMPLATE.md
+-- README.md
```

## Local Web App Check

```bash
cd webapp
npm install
npm start
```

Open `http://localhost:8080`.

Without `FUNCTION_START_URL`, the UI should load but submitting an order should show a configuration error. That is expected until your Azure Function is deployed and wired.

