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
                withCredentials([azureServicePrincipal(
                    credentialsId: 'azure-credentials', 
                    subscriptionIdVariable: 'AZURE_SUBSCRIPTION_ID', 
                    clientIdVariable: 'AZURE_CLIENT_ID', 
                    clientSecretVariable: 'AZURE_CLIENT_SECRET', 
                    tenantIdVariable: 'AZURE_TENANT_ID'
                )]) {
                    bat '''
                        az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET --tenant $AZURE_TENANT_ID
                        az account set --subscription $AZURE_SUBSCRIPTION_ID
                        az webapp deploy --resource-group myResourceGroup --name myAppServiceName --src-path target/*.jar --type jar
                    '''
                }
            }
        }
    }
}
