pipeline {
    agent any
    tools {
        // need to be enable in Jenkins > Tools : Add Maven 'M3'
        maven 'M3'
    }
    stages {
        stage('Fetch Code') {
            steps {
                echo "git code fetched."
            }
        }
        stage('Build code'){
            steps {
                echo "Cleaning dependencies"
                sh "mvn clean install"
            }
        }
    }
}