# Jenkins Learning Demo

Welcome! This repository is designed for beginners who want to learn **Jenkins** and **CI/CD Pipelines**. It contains sample code and documentation to help you understand the core concepts and get hands-on experience.

## 📂 Repository Structure

- **[Jenkinsfile.basic](./Jenkinsfile.basic)**: A simple declarative pipeline to get you started.
- **[Jenkinsfile.docker](./Jenkinsfile.docker)**: A pipeline demonstrating how to run builds inside Docker containers (isolating your build environment).
- **[Jenkinsfile.advanced](./Jenkinsfile.advanced)**: A real-world example featuring parameters, environment variables, parallel execution, and post-build actions.
- **[docs/](./docs/)**:
  - **[THEORY.md](./docs/THEORY.md)**: A detailed guide on What, Why, and How Jenkins works. Read this first!
  - **[INTERVIEW_QUESTIONS.md](./docs/INTERVIEW_QUESTIONS.md)**: Common interview questions and answers to help you prepare for jobs.

## 🚀 How to Use This Repo

1.  **Read the Theory**: Start with `docs/THEORY.md` to build your mental model of Jenkins.
2.  **Analyze the Code**: Open `Jenkinsfile.basic`. Read the comments to understand the syntax.
3.  **Run it in Jenkins**:
    - Install Jenkins (or run it via Docker).
    - Create a "New Item" -> "Pipeline".
    - In the Pipeline definition, you can choose "Pipeline script from SCM" and point it to this repo, or simpler yet, just copy-paste the content of `Jenkinsfile.basic` into the distinct "Pipeline script" box to test it immediately.
4.  **Experiment**: Try modifying the `echo` statements or adding a new stage in the Jenkinsfiles.

## 🤝 Contributing
Feel free to fork this repo and submit Pull Requests if you want to add more examples!

Happy Learning! 