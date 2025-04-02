# **AccuKnox SAST**

## 🔍 **Automate Your Security with SAST Scanning**

The **AccuKnox SAST GitHub Action** seamlessly integrates **Static Application Security Testing (SAST)** into your CI/CD workflows. It leverages **SonarQube** to analyze source code for security vulnerabilities and uploads findings to the **AccuKnox Console**, ensuring comprehensive security insights.

---

## 🎯 **Key Features**

✅ **Automated Code Security Analysis** – Detects security vulnerabilities using SonarQube.  
✅ **Seamless CI/CD Integration** – Easily integrates into GitHub workflows.  
✅ **Centralized Security Insights** – Uploads findings to AccuKnox Console.  
✅ **Quality Gate Enforcement** – Blocks insecure code from merging.  
✅ **Customizable Parameters** – Configure project-specific security settings.  

---

## ⚠️ **Prerequisites**

Before using this GitHub Action, ensure the following:

1️⃣ **An AccuKnox Account** – Required for accessing the AccuKnox Console.  
2️⃣ **SonarQube Setup** – A working SonarQube instance for static analysis.  
3️⃣ **GitHub Repository with Actions Enabled** – Required to run workflows.  
4  **AccuKnox API Token & Tenant ID** – Required for authentication (see [Token Generation](https://help.accuknox.com/getting-started/how-to-create-tokens/)).  

---

## 📌 **Installation & Usage**

### **Step 1: Configure SonarQube Properties**

Create a `sonar-project.properties` file in the root directory with the following configuration:

```properties
sonar.projectKey=my-project-key
sonar.organization=my-organization
sonar.host.url=${{ secrets.SONAR_HOST_URL }}
sonar.login=${{ secrets.SONAR_TOKEN }}
```

🔹 Replace `my-project-key` and `my-organization` with your actual **SonarQube** project details.

### **Step 2: Retrieve AccuKnox API Credentials**

To authenticate with **AccuKnox Console**, retrieve the required credentials from the **AccuKnox Console**:


1️⃣ **Go to Settings** → Navigate to the **Tokens** section in the **AccuKnox Console**.  
2️⃣ **Create a New Token** → Click on **Create Token** to generate `accuknox_token` and `tenant_id`.  
3️⃣ **Store Securely** → Copy and securely store these credentials for workflow usage.  

### **Step 3: Implement the Workflow YAML**

Create a workflow file `.github/workflows/accuknox-sast.yml` and add the following configuration:

```yaml
name: AccuKnox SAST Scan

on:
  push:
    branches:
      - main

jobs:
  sast-scan:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v2

      - name: Run AccuKnox SAST Scan
        uses: accuknox/sast-scan-action@v1.0.0
        with:
          sonar_token: ${{ secrets.SONAR_TOKEN }}
          sonar_host_url: ${{ secrets.SONAR_HOST_URL }}
          accuknox_endpoint: ${{ secrets.ACCUKNOX_ENDPOINT }}
          tenant_id: ${{ secrets.TENANT_ID }}
          accuknox_token: ${{ secrets.ACCUKNOX_TOKEN }}
          label: "my-sast-scan"
          sonar_project_key: "my-project-key"

```

---

## ⚙️ **Configuration Options (Inputs)**

| **Parameter**        | **Description**                                      | **Required** | **Default Value** |
|----------------------|------------------------------------------------------|--------------|-------------------|
| `sonar_token`       | SonarQube authentication token.                      | ✅ Yes       | None              |
| `sonar_host_url`    | SonarQube server URL.                                | ✅ Yes       | None              |
| `accuknox_endpoint` | AccuKnox API endpoint for uploading results.         | ✅ Yes       | None              |
| `tenant_id`         | Unique ID of the AccuKnox Console.               | ✅ Yes       | None              |
| `accuknox_token`    | API token for AccuKnox authentication.               | ✅ Yes       | None              |
| `label`             | Tagging label for scan results in AccuKnox Console.          | ✅ Yes       | None              |
| `sonar_project_key` | SonarQube project key for tracking the scan.         | ✅ Yes       | None              |

---

## 🔍 **How It Works?**

### **Step 1: Code Analysis**
- SonarQube scans your repository’s source code for vulnerabilities.

### **Step 2: Report Processing**
- The AccuKnox SAST GitHub Action formats the scan results for better security insights.
git@github.com:udit-uniyal/sast-scan-action.git
### **Step 3: Findings Upload**
- The scan results are automatically sent to **AccuKnox Console** for centralized security tracking.

### **Step 4: Quality Gate Enforcement**
- If security issues exceed the defined threshold, the pipeline fails, preventing insecure code from merging.

---

## 🛠️ **Troubleshooting & Best Practices**

### ❌ **Pipeline Failing Due to Vulnerabilities?**
- Adjust the **quality gate settings** to allow lower severity issues.  
- Use **SonarQube’s exclusion rules** to filter out non-critical findings.  

### 🔑 **Invalid Token Error?**
- Ensure your **API tokens are correctly set** in GitHub Secrets.  
- **Regenerate** the token from the AccuKnox Console if needed.  

---

## 🔒 **Security Best Practices**

- **Regular Scans** – Automate scanning on every pull request & deployment.  
- **Enforce Policies** – Set **quality gates** to prevent high-risk vulnerabilities.  
- **Least Privilege Access** – Store secrets securely in GitHub Secrets.  

---

## 📖 **Support & Documentation**

📚 **Read More:** [AccuKnox Docs](https://help.accuknox.com/)  
📧 **Contact Support:** [support@accuknox.com](mailto:support@accuknox.com)  

---

## 🏆 **Conclusion**

The **AccuKnox SAST GitHub Action** enables teams to **detect vulnerabilities early**, enforce security best practices, and seamlessly integrate security testing into CI/CD pipelines. 

> 🔹 **Enhance Your DevSecOps Pipeline with AccuKnox SAST – Start Today!** 🔒


