# Calculator App (Java + Maven + Jenkins)

Simple Java calculator with JUnit 5 tests and a Jenkins pipeline.

## Run locally
```bash
mvn clean test          # build + run tests
mvn package             # create jar
java -jar target/calculator-app-1.0.0.jar
```

## 1. Push to GitHub
Create an empty repo on GitHub (e.g. `calculator-app`), then:
```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/<your-username>/calculator-app.git
git push -u origin main
```

## 2. Configure Jenkins tools (one time)
Manage Jenkins > Tools:
- **JDK** installation named `JDK17`
- **Maven** installation named `Maven3`

Plugins needed: Git, Pipeline, JUnit (all included in the suggested plugins).

## 3. Create the Jenkins job
1. New Item > name `calculator-app` > **Pipeline** > OK
2. Pipeline section > Definition: **Pipeline script from SCM**
3. SCM: **Git**, Repository URL: your GitHub repo URL
   (add credentials — a GitHub personal access token — if the repo is private)
4. Branch: `*/main`, Script Path: `Jenkinsfile`
5. Save > **Build Now**

Stages: Checkout > Build > Test (JUnit report) > Package (jar archived) > Run.

## Optional: auto-build on every push
- Job > Configure > Build Triggers > tick **GitHub hook trigger for GITScm polling**
- GitHub repo > Settings > Webhooks > add `http://<jenkins-url>/github-webhook/` (content type `application/json`)
