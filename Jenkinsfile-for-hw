pipeline {
    agent any
    tools {
        // need to be enable in Jenkins > Tools : Add Maven 'M3'
        maven 'M3'
    }
    stages {
        stage('Fetch Code') {
            steps {
                echo 'git code fetched.'
            }
        }

        stage('Build code') {
            steps {
                dir('hw') {
                    echo 'Cleaning dependencies'
                    sh 'mvn clean install'
                }
            }
        }

// nexusArtifactUploader credentialsId: 'nexus-jenkins', groupId: 'org.springframework.boot', nexusUrl: 'urban-fiesta-v557p495wq7hxwjv-8081.app.github.dev/repository/echrev1-dev/', nexusVersion: 'nexus2', protocol: 'http', repository: 'echrev1-dev', version: '0.0.1-SNAPSHOT'

        stage('Send to Nexus snapshot rep') {
            steps {
                dir('hw') {
                    echo 'Nexus upload'
                    nexusArtifactUploader(
                        credentialsId: 'nexus-jenkins',
                        // credentialsId: 'jenkins-admin',
                        groupId: 'com.example',
                        nexusUrl: 'urban-fiesta-v557p495wq7hxwjv-8081.app.github.dev',
                        // nexusUrl: 'urban-fiesta-v557p495wq7hxwjv-8081.app.github.dev/repository/echrev1-dev/',
                        nexusVersion: 'nexus3',
                        protocol: 'https',
                        repository: 'echrev1-dev',
                        version: '1.0-SNAPSHOT',
                        artifacts: [
                            [
                                artifactId: 'hello-world-cli', 
                                classifier: '', 
                                file: 'target/hello-world-cli-1.0-SNAPSHOT.jar', 
                                type: 'jar'
                            ]
                        ]
                        )
                }
            }
        }
    }
}
