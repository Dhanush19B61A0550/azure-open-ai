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
                withCredentials([
                    usernamePassword(credentialsId: 'AZURE_SERVICE_PRINCIPAL', 
                                     usernameVariable: 'AZURE_SERVICE_PRINCIPAL', 
                                     passwordVariable: 'AZURE_CREDENTIALS_PASSWORD'),
                    usernamePassword(credentialsId: 'AZURE_CREDENTIALS_TENANT', variable: 'AZURE_CREDENTIALS_TENANT')
                ]) {
                    echo "Logging into Azure with Service Principal."

                    bat '''
                    az login --service-principal -u %AZURE_SERVICE_PRINCIPAL% -p %AZURE_CREDENTIALS_PASSWORD% --tenant %AZURE_CREDENTIALS_TENANT%
                    az webapp deploy --resource-group dhana --name backend-ai --src-path target/*.jar --type jar
                    '''
                }
            }
        }
    }
}
