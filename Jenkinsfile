pipeline {
    agent any
    environment {
        AZURE_CREDENTIALS = credentials('azure-service-principal')
    }
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
                script {
                    if (!env.AZURE_CREDENTIALS) {
                        error('Azure credentials are not set. Please configure the AZURE_CREDENTIALS variable in Jenkins.')
                    }
                }
                bat '''
                az login --service-principal -u $AZURE_CREDENTIALS_USR -p $AZURE_CREDENTIALS_PSW --tenant $AZURE_CREDENTIALS_TENANT
                az webapp deploy --resource-group <RESOURCE_GROUP_NAME> --name <APP_SERVICE_NAME> --type jar --src-path target/*.jar
                '''
            }
        }
    }
}
