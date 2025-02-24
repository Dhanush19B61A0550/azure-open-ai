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
    // stage('Deploy') {
    // steps {
    //     withCredentials([usernamePassword(credentialsId: 'AZURE_SERVICE_PRINCIPAL', variable: 'AZURE_SERVICE_PRINCIPAL'),
    //                      usernamePassword(credentialsId: 'AZURE_CREDENTIALS_PASSWORD', variable: 'AZURE_CREDENTIALS_PASSWORD'),
    //                      usernamePassword(credentialsId: 'AZURE_CREDENTIALS_TENANT', variable: 'AZURE_CREDENTIALS_TENANT')]) {
    //         // echo $AZURE_SERVICE_PRINCIPAL
            // echo $AZURE_CREDENTIALS_PASSWORD
            // echo $AZURE_CREDENTIALS_TENANT
            // bat '''
            // az login --service-principal -u $AZURE_SERVICE_PRINCIPAL -p $AZURE_CREDENTIALS_PASSWORD --tenant $AZURE_CREDENTIALS_TENANT
            // az webapp deploy --resource-group dhana --name backend-ai --src-path target/*.jar --type jar
            // '''

echo "hii"
 // bat '''
 //            az login --service-principal -u %AZURE_SERVICE_PRINCIPAL% -p %AZURE_CREDENTIALS_PASSWORD% --tenant %AZURE_CREDENTIALS_TENANT%
 //            az webapp deploy --resource-group dhana --name backend-ai --src-path target/*.jar --type jar
 //            '''


stage('Deploy') {
    steps {
        withCredentials([
            usernamePassword(credentialsId: 'azure_service_principle', 
                             usernameVariable: 'AZURE_SERVICE_PRINCIPAL', 
                             passwordVariable: 'AZURE_CREDENTIALS_PASSWORD'),
            string(credentialsId: 'AZURE_CREDENTIALS_TENANT', variable: 'AZURE_CREDENTIALS_TENANT')
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
}
    
    
    
    
    }
}
