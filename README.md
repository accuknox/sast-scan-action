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
4️⃣ **AccuKnox API Token & Tenant ID** – Required for authentication (see [Token Generation](https://help.accuknox.com/getting-started/how-to-create-tokens/)).  

## 📌 **Installation & Usage**

### **Step 1: Configure SonarQube Properties**

1️⃣ Get **SonarQube** project details and credentials from the **SonarQube** instance
2️⃣ Store Securely → Copy and securely store these credentials for workflow usage.

### **Step 2: Retrieve AccuKnox API Credentials**

To authenticate with **AccuKnox Console**, retrieve the required credentials from the **AccuKnox Console**:

1️⃣ **Go to Settings** → Navigate to the **Tokens** section in the **AccuKnox Console**.

2️⃣ **Create a New Token** → Click on **Create Token** to generate `accuknox_token`. 

3️⃣ **Store Securely** → Copy and securely store these credentials for workflow usage.  

### **Step 3: Implement the Workflow YAML**

Create a workflow file `.github/workflows/accuknox-sast.yml` and add the following configuration:

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
        uses: actions/checkout@v4

      - name: Run AccuKnox SAST
        uses: accuknox/sast-scan-action@latest
        with:
          skip_sonar_scan: false
          sonar_project_key: ${{ secrets.SONAR_PROJECT_KEY }}
          sonar_token: ${{ secrets.SONAR_TOKEN }}
          sonar_host_url: ${{ secrets.SONAR_HOST_URL }}
          sonar_organization_id: ${{ secrets.SONAR_ORG_ID }}
          accuknox_endpoint: ${{ secrets.ACCUKNOX_ENDPOINT }}
          accuknox_token: ${{ secrets.ACCUKNOX_TOKEN }}
          accuknox_label: ${{ secrets.ACCUKNOX_LABEL }}
          soft_fail: false
```

## ⚙️ **Configuration Options (Inputs)**

| Input Value        | Description                                                | Optional/Required | Default Value |
|--------------------|------------------------------------------------------------|--------------------|---------------|
| `sonar_token`      | Personal access token for authenticating with SonarQube.   | Required          | None          |
| `sonar_host_url`   | URL of the SonarQube server to run the SAST.               | Required          | None          |
| `accuknox_endpoint`| AccuKnox API endpoint URL to upload the scan results.      | Required          | None          |
| `accuknox_token`   | Token for authenticating with AccuKnox API.                | Required          | None          |
| `accuknox_label`   | Label in AccuKnox SaaS for tagging scan results.           | Required          | None          |
| `sonar_project_key`| Project key in SonarQube for identifying the project.      | Required          | None          |
| `sonar_organization_id`| Organisation ID for SonarQube (For cloud user only).       | Optional          | None          |
| `skip_sonar_scan`  | Skip SonarQube scan, for advanced users                    | Optional          | false          |
| `soft_fail`        | Do not return an error code if there are failed checks.    | Optional          | false          |


## 🔍 **How It Works?**

### **Step 1: Code Analysis**
- SonarQube scans your repository’s source code for vulnerabilities.

### **Step 2: Report Processing**
- The AccuKnox SAST GitHub Action formats the scan results for better security insights.

### **Step 3: Findings Upload**
- The scan results are automatically sent to **AccuKnox Console** for centralized security tracking.

### **Step 4: Quality Gate Enforcement**
- The pipeline fails if security issues exceed the defined threshold, preventing insecure code from merging.

---

## 🛠️ **Troubleshooting & Best Practices**

### ❌ **Pipeline Failing Due to Vulnerabilities?**
- Adjust the **quality gate settings** to allow lower-severity issues.  
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
