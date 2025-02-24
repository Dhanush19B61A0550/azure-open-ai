pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    bat 'mvn clean package'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    bat 'mvn test'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    withCredentials([azureServicePrincipal('AZURE_CREDENTIALS_ID')]) {
                        bat '''
                        az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET --tenant $AZURE_TENANT_ID
                        az webapp deploy --name YOUR_APP_SERVICE_NAME --resource-group YOUR_RESOURCE_GROUP --src-path target/*.war
                        '''
                    }
                }
            }
        }
    }
}
