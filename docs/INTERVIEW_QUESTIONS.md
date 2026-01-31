# Jenkins Interview Questions & Answers

## Beginner Level

### Q1: What is the difference between Continuous Integration (CI) and Continuous Delivery (CD)?
**A:**
- **CI (Continuous Integration)**: The practice of automatically building and testing code every time a team member commits changes to version control. The goal is to detect integration errors as quickly as possible.
- **CD (Continuous Delivery)**: Extends CI by ensuring that the software can be released to production at any time. It automates the release process up to the production deployment step (which may still be manual).
- **Continuous Deployment**: Goes one step further—every change that passes all stages of the pipeline is released to production automatically, with no human intervention.

### Q2: What is a `Jenkinsfile`?
**A:** A text file that stores the entire workflow of the Jenkins pipeline as code. It is checked into the SCM (Source Control Management) like Git. This practice is known as "Pipeline as Code." It allows the build process to be versioned and reviewed just like the application code.

### Q3: How do you install Jenkins?
**A:**
1.  Run the `.war` file directly: `java -jar jenkins.war`
2.  Run as a system service (Windows Service, Linux Package).
3.  **Docker (Most popular now)**: `docker run -p 8080:8080 -p 50000:50000 jenkins/jenkins:lts`

---

## Intermediate Level

### Q4: Explain the architecture of Jenkins (Master-Slave/Controller-Agent).
**A:** Jenkins uses a distributed architecture.
- **Controller (Master)**: Manages the configuration, schedules jobs, serves the UI, and dispatches tasks to agents. It holds the build history.
- **Agents (Slaves)**: Small Java programs running on remote machines (or containers) effectively doing the heavy lifting. They execute the build steps requested by the Controller. This allows Jenkins to scale and support different operating systems for different builds.

### Q5: What is the difference between Declarative and Scripted Pipelines?
**A:**
- **Scripted Pipeline**: Traditional way, uses strict Groovy syntax. Very flexible and powerful but harder to write and maintain.
- **Declarative Pipeline**: Newer, more structured syntax. Easier to read and write. It provides a predefined structure (`pipeline {}`, `stages {}`, `steps {}`) and is the industry standard for most use cases today.

### Q6: How do you manually approve a deployment in a pipeline?
**A:** By using the `input` step in the pipeline.
```groovy
stage('Deploy to Prod') {
    steps {
        input message: 'Approve deployment?', ok: 'Yes'
        sh './deploy.sh'
    }
}
```
The pipeline pauses at this step until a user clicks "Proceed" in the UI.

---

## Real-World Scenarios

### Q7: The build is failing, but it works on my local machine. What do I do?
**A:** This is a classic environment issue.
1.  Check the "Console Output" in Jenkins to identify the exact error.
2.  Verify the Jenkins Agent environment (Java version, Node version, connection to DB) matches your local setup.
3.  Check if you committed all necessary files (maybe a config file is git-ignored but needed for the build).
4.  Use `Jenkinsfile.docker` (Docker Agents) to ensure the build runs in a container identical to your local dev environment.

### Q8: How do you handle secrets (passwords, API keys) in Jenkins?
**A:** **NEVER** hardcode credentials in the `Jenkinsfile`.
1.  Go to **Manage Jenkins > Manage Credentials**.
2.  Add a generic username/password or "Secret Text".
3.  In the pipeline, use the `credentials()` helper or `withCredentials` block to inject them safely into environment variables during the build.

### Q9: How can checking out a git repository be triggered automatically?
**A:**
1.  **Polling SCM**: Jenkins checks Git every X minutes for changes (Resource intensive, not recommended).
2.  **Webhooks (Best Practice)**: Configure a Webhook in GitHub/Bitbucket to send a POST request to Jenkins whenever a push occurs. Jenkins then immediately triggers the build.
