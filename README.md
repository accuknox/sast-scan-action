# AccuKnox SAST GitHub Action

## Learn More

- [About Accuknox](https://www.accuknox.com/)

**Description**  
This GitHub Action runs a Static Application Security Testing (SAST) using SonarQube, then uploads the generated report to the AccuKnox CSPM panel. The action can be configured with specific inputs to integrate seamlessly with your DevSecOps pipeline.

## Usage

### Steps for Using AccuKnox SAST Scan Action in a Workflow YAML File

1. **Checkout into the Repo**  
   Use the checkout action to ensure your codebase is available for scanning.

2. **Add AccuKnox SAST Scan Action**  
   Use the `accuknox/accuknox-sast@v1.0.1` repository with the desired version tag, e.g., `v1.0.1`.

3. **Token Generation from AccuKnox SaaS and Viewing Tenant ID**  
   To obtain the `accuknox_token` and `tenant_id` values needed to authenticate with AccuKnox:
   
   - **Navigate to Tokens**  
     Go to the **Settings** section in the AccuKnox SaaS sidebar.

     ![1](https://github.com/udit-uniyal/container-scan-action/assets/115368361/8f4e188b-d9f3-4404-83af-134d5dc1417a)
   
   - **Create Token**  
     In the "Tokens" section, click on **Create Token**. This action will display your `tenant_id` and allow you to generate an access token.

     ![2](https://github.com/udit-uniyal/container-scan-action/assets/115368361/296bc611-acb8-4918-9d6b-3a8ec7733377)
   
   - **Generate the Token**  
     After clicking **Generate**, copy the `accuknox_token` to use in the workflow.

   ![3](https://github.com/udit-uniyal/container-scan-action/assets/115368361/16032af0-bcac-4787-8f2a-a3fa0edc6ec6)

### Example Workflow File

```yaml
name: AccuKnox SAST Workflow
on:
  push:
    branches:
      - main

jobs:
  sast-scan:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Run AccuKnox SAST
        uses: accuknox/sast-scan-action@v1.0.0
        with:
          sonar_token: ${{ secrets.SONAR_TOKEN }}
          sonar_host_url: ${{ secrets.SONAR_HOST_URL }}
          sonar_project_key: "my-project-key"
          accuknox_endpoint: ${{ secrets.ACCUKNOX_ENDPOINT }}
          accuknox_token: ${{ secrets.ACCUKNOX_DEV_TOKEN }}
          tenant_id: TENANT_ID
          label: "my-sast-scan"
          input_soft_fail: false
          skip_sonar_scan: false
```

## Input Values

| Input Value        | Description                                                | Optional/Required | Default Value |
|--------------------|------------------------------------------------------------|--------------------|---------------|
| `sonar_token`      | Personal access token for authenticating with SonarQube.   | Required          | None          |
| `sonar_host_url`   | URL of the SonarQube server to run the SAST.               | Required          | None          |
| `accuknox_endpoint`| AccuKnox API endpoint URL to upload the scan results.      | Required          | None          |
| `tenant_id`        | Unique ID of the tenant for AccuKnox CSPM panel.           | Required          | None          |
| `accuknox_token`   | Token for authenticating with AccuKnox API.                | Required          | None          |
| `label`            | Label in AccuKnox SaaS for tagging scan results.           | Required          | None          |
| `sonar_project_key`| Project key in SonarQube for identifying the project.      | Required          | None          |
| `sonar_organization_id`| Organization ID for SonarQube (For cloud user only).       | Optional          | None          |
| `skip_sonar_scan`  | Skip SonarQube scan, for advanced users                    | Optional          | false          |
| `input_soft_fail`  | Do not return an error code if there are failed checks.    | Optional          | false          |
| `upload_artifact`  | Upload scan results as artifact	                          | Optional          | false          |

## How it Works

- **SonarQube SAST**: The action runs a SAST scan on the specified project in SonarQube, using the provided credentials and project key.
- **AccuKnox Report Generation**: The action uses AccuKnox's Docker container to generate a SAST report.
- **Report Upload**: The generated report is uploaded to the AccuKnox CSPM panel for centralized monitoring and insights.
- **Quality Gate Check**: Verifies if the project meets the set quality standards on SonarQube.

## Notes

- Ensure all necessary secrets (`SONAR_TOKEN`, `SONAR_HOST_URL`, `ACCUKNOX_ENDPOINT`, `TENANT_ID`, and `ACCUKNOX_TOKEN`) are securely stored in your repository's settings.
- AccuKnox panel provides a centralized view of all SAST results, enabling detailed security monitoring and analytics.
  
