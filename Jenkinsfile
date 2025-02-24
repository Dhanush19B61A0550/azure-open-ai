Below is a Jenkinsfile for deploying a Java backend using Maven and Azure App Service. The Jenkins pipeline includes three stages: Build, Test, and Deploy.

```groovy
pipeline {
    agent any

    environment {
        // Define environment variables
        AZURE_APP_NAME = 'your-azure-app-name'  // Replace with your Azure App Service name
        AZURE_RESOURCE_GROUP = 'your-resource-group'  // Replace with your Azure Resource Group
        MAVEN_HOME = tool 'Maven'  // Jenkins Maven tool installation name
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                sh "${MAVEN_HOME}/bin/mvn clean package -DskipTests"
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh "${MAVEN_HOME}/bin/mvn test"
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo 'Deploying to Azure App Service...'
                    def warFile = findFiles(glob: 'target/*.war')[0].path
                    // Deploy the WAR file using Azure CLI
                    sh """
                        az webapp deploy --resource-group ${AZURE_RESOURCE_GROUP} \
                        --name ${AZURE_APP_NAME} \
                        --src-path ${warFile} \
                        --type war
                    """
                }
            }
        }
    }

    post {
        always {
            echo 'Cleaning up workspace...'
            cleanWs()
        }

        success {
            echo 'Deployment succeeded!'
        }

        failure {
            echo 'Deployment failed.'
        }
    }
}
```

### Explanation:
1. **Build Stage**:
   - Runs `mvn clean package -DskipTests` to compile the Java code and package it as a `.war` file, skipping tests during the build.

2. **Test Stage**:
   - Executes `mvn test` to run the unit tests and ensure the code is functioning as expected.

3. **Deploy Stage**:
   - Finds the `.war` file in the `target/` directory.
   - Uses the Azure CLI (`az webapp deploy`) to deploy the `.war` file to Azure App Service.

4. **Post Actions**:
   - Always cleans up the workspace to remove unused files and ensure a fresh start for the next build.
   - Reports whether the deployment succeeded or failed.

### Prerequisites:
- Make sure the Azure CLI is installed and configured on the Jenkins agent.
- Authenticate the Azure CLI with a service principal or logged-in user.
- Replace `your-azure-app-name` and `your-resource-group` with your Azure App Service and resource group names.
- Ensure Maven is installed and configured as a Jenkins tool.

This pipeline automates the build, test, and deployment processes for your Java backend to Azure App Service.
