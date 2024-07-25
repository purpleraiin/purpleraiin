SonarQube
SonarQube is an open-source platform developed by SonarSource for continuous inspection of code quality. It performs automatic reviews of code to detect bugs, vulnerabilities, and code smells in applications. SonarQube supports a wide range of programming languages, including Scala, Python, yml, XML, Java, C#, JavaScript, TypeScript, C++, and many others.
What SonarQube Provides
* Static Code Analysis: SonarQube analyzes the source code without executing it, identifying potential issues early in the development cycle.
* Code Quality Metrics: It provides various metrics that help measure code quality, including complexity, duplication, code coverage, and more.
* Issue Tracking: It detects and tracks issues such as bugs, vulnerabilities, and code smells, categorizing them by severity (blocker, critical, major, minor, info).
* Quality Gates: Quality gates are a set of conditions that code must meet before being considered of acceptable quality. They can include thresholds for code coverage, duplications, critical issues, and more.
* Visualization Tools: SonarQube offers dashboards and detailed visual reports to help developers understand the state of their codebase.
* Integration: It integrates seamlessly with various build tools and CI/CD pipelines, including Jenkins, Azure DevOps, GitHub Actions, and more.
* Customization: Rules and quality profiles can be customized to fit the specific needs of a project or organization.
* Security Reports: SonarQube provides detailed security reports, highlighting potential vulnerabilities in the codebase.
Benefits and Advantages of SonarQube
* Early Detection of Issues: SonarQube helps identify bugs, vulnerabilities, and code smells early in the development process, reducing the cost and effort required to fix them later.
* Enhanced Security: SonarQube detects security vulnerabilities and provides guidance on how to fix them, helping to improve the overall security of the application.
* Increased Developer Productivity: Automated code reviews save developers time and effort, allowing them to focus on writing new code rather than manually checking for issues.
* Standardization: By enforcing coding standards and best practices, SonarQube helps standardize code quality across different teams and projects.
* Continuous Improvement: Regular use of SonarQube encourages a culture of continuous improvement, with teams constantly striving to improve their code quality.
* Integration with DevOps: Seamless integration with CI/CD pipelines ensures that code quality checks are an integral part of the development workflow, providing immediate feedback to developers.
Overall, SonarQube is a powerful tool for maintaining high code quality, improving security, and ensuring that code remains maintainable and robust over time.
Prerequisites
* SonarQube Server: Ensure you have a running instance of SonarQube server.
* SonarQube Extension: Install the SonarQube extension from the Azure DevOps Marketplace.
* SonarQube Service Connection: Set up a service connection to your SonarQube server in Azure DevOps.
Configure Pipeline with Classic Editor
1. Open Classic Editor:
2. Add SonarQube Tasks:
* Prepare Analysis Configuration:
    * Click the "+" button to add a new task.
    * Search for "SonarQube" and select "Prepare Analysis Configuration".
    * Configure the task with your SonarQube service connection and provide project details.
￼
* Run Code Analysis:
    * Add another task by clicking the "+" button.
    * Search for "SonarQube" and select "Run Code Analysis".
    * No additional configuration is needed here.
* Publish Quality Gate Result:
    * Add another task by clicking the "+" button.
    * Search for "SonarQube" and select "Publish Quality Gate Result".
    * Configure the task with your SonarQube service connection.
3. Build Steps:
* Ensure the "Prepare Analysis Configuration" task is before your build steps.
* The "Run Code Analysis" task should run after your build steps.
* The "Publish Quality Gate Result" task should run after the code analysis.
4. Save and Queue:
* Save your pipeline configuration.
* Queue a new build to test the integration.
NOTE : sonar-project.properties file need to save in paraticular branch in order to get it scan over sonarqube.
SonarQube URL:
http://sonar3.jio.com:9000/projects 
￼
here as you can see we can successfully able to scan the coe-ingestion-cdp-integration repo via build pipeline as we have store sonar-project.properties file in master and added plugins into build pipeline.
sonar.host.url=http://sonar3.jio.com:9000/
sonar.java.binaries=.
sonar.sources=.
sonar.branch.name=master
sonar.branch.longLivedBranches.regex=master
sonar.exclusions=src/assets/**,src/environments/**
sonar.projectKey=coe-ingestion-cdp-integration	
sonar.projectName=coe-ingestion-cdp-integration	
sonar.projectVersion=1.0
sonar.sourceEncoding=UTF-8
If any developer want to scan any other branch than master they need to create sonar-project.properties in that branch (Don't create that inside any folder kept it outside only). Also need to change below property
FROM
sonar.branch.name=master
TO
sonar.branch.name=(any other branch name)

Example

sonar.branch.name=cdp_dev
On sonarqube developer will able to see code analysis for other branch as well.
￼

Conclusion
By following these steps, you will have successfully integrated SonarQube with your Azure DevOps pipeline, ensuring that your builds are automatically analyzed for code quality and that the pipeline will fail if the quality gate criteria are not met. This setup helps maintain high code quality and early detection of potential issues in your codebase.
