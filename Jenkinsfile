pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                withCredentials([azureServicePrincipal('AZURE_CREDENTIALS')]) {
                    sh '''
                        az login --service-principal -u $AZURE_CREDENTIALS_USR -p $AZURE_CREDENTIALS_PSW --tenant $AZURE_CREDENTIALS_TENANT
                        az webapp deploy --resource-group <RESOURCE_GROUP> --name <APP_SERVICE_NAME> --src-path target/*.war --type war
                    '''
                }
            }
        }
    }
}
