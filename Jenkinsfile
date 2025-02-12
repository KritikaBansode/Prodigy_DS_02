pipeline {
    agent any  

    tools {
        maven 'MAVEN'  // Make sure 'MAVEN' is the exact name from Jenkins Global Tool Configuration
        jdk 'JDK'      // Make sure 'JDK' is the exact name from Jenkins Global Tool Configuration
    }

    stages {
        stage('Initialize') {
            steps {
                echo "Setting up environment variables"
                echo "Maven Home: ${tool 'MAVEN'}"
            }
        }

        stage('Check Java Version') {  
            steps {
                sh 'java -version'  // Verify Java installation
            }
        }

        stage('Build') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'chmod +x mvnw'  // Ensures the script has execute permission on Linux
                        sh './mvnw -B -DskipTests clean package'  // Runs Maven build on Linux
                    } else {
                        bat 'mvnw -B -DskipTests clean package'  // Runs Maven build on Windows
                    }
                }
            }
        }
    }

    post {
        always {
            junit(
                allowEmptyResults: true,
                testResults: '*/test-reports/*.xml'
            )
        }
    }
}
