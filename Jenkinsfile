pipeline {
    agent any
    tools {
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
                dir('simple-rest-api') {
                    echo 'Cleaning dependencies'
                    sh 'mvn clean package'
                }
            }
        }

        stage('Read POM Values') {
            steps {
                script {
                    // Read the POM file
                    def pom = readMavenPom(file: 'simple-rest-api/pom.xml')
                    
                    // Extract values
                    def version = pom.version
                    def groupId = pom.groupId
                    def artifactId = pom.artifactId
                    
                    // Print extracted values for verification
                    echo "Version: ${version}"
                    echo "Group ID: ${groupId}"
                    echo "Artifact ID: ${artifactId}"
                }
            }
        }

        stage('Send to Nexus snapshot rep') {
            steps {
                dir('simple-rest-api') {
                    echo 'Nexus upload'
                    nexusArtifactUploader(
                        credentialsId: 'nexus-jenkins',
                        groupId: groupId,
                        nexusUrl: 'urban-fiesta-v557p495wq7hxwjv-8081.app.github.dev',
                        nexusVersion: 'nexus3',
                        protocol: 'https',
                        repository: 'echrev1-dev',
                        version: version,
                        artifacts: [
                            [
                                artifactId: artifactId, 
                                classifier: '', 
                                file: "target/${artifactId}-${version}.jar", 
                                type: 'jar'
                            ]
                        ]
                    )
                }
            }
        }
    }
}
