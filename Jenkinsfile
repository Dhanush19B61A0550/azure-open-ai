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
        // stage('Deploy') {
        //     steps {
        //         withCredentials([string(credentialsId: 'AZURE_SERVICE_PRINCIPAL', variable: 'AZURE_CREDENTIALS')]) {
        //             bat '''
        //             az login --service-principal -u $AZURE_SERVICE_PRINCIPAL -p $AZURE_CREDENTIALS_PASSWORD --tenant $AZURE_CREDENTIALS_TENANT
        //             az webapp deploy --resource-group myResourceGroup --name myAppService --src-path target/*.jar --type jar
        //             '''
        //         }
        //    }
    stage('Deploy') {
    steps {
        withCredentials([string(credentialsId: 'AZURE_SERVICE_PRINCIPAL', variable: 'AZURE_SERVICE_PRINCIPAL_ID'),
                         string(credentialsId: 'AZURE_CREDENTIALS_PASSWORD', variable: 'AZURE_CREDENTIALS_PASSWORD'),
                         string(credentialsId: 'AZURE_CREDENTIALS_TENANT', variable: 'AZURE_CREDENTIALS_TENANT')]) {
            bat '''
            az login --service-principal -u $AZURE_SERVICE_PRINCIPAL_ID -p $AZURE_CREDENTIALS_PASSWORD --tenant $AZURE_CREDENTIALS_TENANT
            az webapp deploy --resource-group dhana --name backend-ai --src-path target/*.jar --type jar
            '''
        }
    }
}
    
    
    
    }
    }
}
