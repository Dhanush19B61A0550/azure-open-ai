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
                    withCredentials([azureServicePrincipal(
                        credentialsId: 'azure-credentials-id',
                        subscriptionIdVariable: 'AZURE_SUBSCRIPTION_ID',
                        clientIdVariable: 'AZURE_CLIENT_ID',
                        clientSecretVariable: 'AZURE_CLIENT_SECRET',
                        tenantIdVariable: 'AZURE_TENANT_ID'
                    )]) {
                        bat '''
                        az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET --tenant $AZURE_TENANT_ID
                        az webapp deploy --resource-group YOUR_RESOURCE_GROUP --name YOUR_APP_SERVICE_NAME --type jar --src-path target/*.jar
                        '''
                    }
                }
            }
        }
    }
}
