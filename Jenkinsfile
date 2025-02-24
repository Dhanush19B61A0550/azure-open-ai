pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                withAzureWebApp(azureCredentialsId: 'your-azure-credentials-id', resourceGroup: 'your-resource-group', appName: 'your-app-service-name') {
                    bat 'az webapp deploy --resource-group your-resource-group --name your-app-service-name --src-path target/*.jar --type jar'
                }
            }
        }
    }
}
