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
            environment {
                AZURE_CREDENTIALS = credentials('azure-service-principal')
            }
            steps {
                script {
                    def jarFile = sh(script: 'ls target/*.jar', returnStdout: true).trim()
                    bat """
                        az login --service-principal -u ${AZURE_CREDENTIALS_USR} -p ${AZURE_CREDENTIALS_PSW} --tenant ${AZURE_CREDENTIALS_TENANT}
                        az webapp deploy --resource-group <RESOURCE_GROUP_NAME> --name <APP_SERVICE_NAME> --src-path ${jarFile}
                    """
                }
            }
        }
    }
}
