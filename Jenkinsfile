pipeline {
    agent any
    environment {
        AZURE_CREDENTIALS = credentials('AZURE_CREDENTIALS')
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
                        error "Azure credentials are not set. Please configure the 'AZURE_CREDENTIALS' credential in Jenkins."
                    }
                }
                bat '''
                    az login --service-principal -u ${AZURE_CREDENTIALS_USR} -p ${AZURE_CREDENTIALS_PSW} --tenant ${AZURE_CREDENTIALS_TENANT}
                    az webapp deploy --name <App_Service_Name> --resource-group <Resource_Group_Name> --src-path target/*.jar --type jar
                '''
            }
        }
    }
    post {
        always {
            echo 'Pipeline execution complete.'
        }
    }
}
