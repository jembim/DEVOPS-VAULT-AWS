pipeline {
    agent { label 'aws' }
    stages {
        stage('Retrieve Secret') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'aws-credentials-id', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')]) {
                    sh '''#!/bin/bash
                        export AWS_DEFAULT_REGION=us-east-1
                        export USERNAME=`aws secretsmanager get-secret-value --secret-id tutorials/MyFirstTutorialSecret --version-stage AWSCURRENT --output text --query 'SecretString' | awk -F '"' '{print $4}'`
                        export PASSWORD=`aws secretsmanager get-secret-value --secret-id tutorials/MyFirstTutorialSecret --version-stage AWSCURRENT --output text --query 'SecretString' | awk -F '"' '{print $8}'`
                        echo $USERNAME
                        echo $PASSWORD
                    '''
                }
            }
        }
    }
}