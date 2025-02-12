pipeline {
    agent any  // Runs on any available Jenkins agent

    tools {
        maven 'MAVEN'  // Ensure 'MAVEN' is the exact name configured in Jenkins
        jdk 'JDK'      // Ensure 'JDK' is the exact name configured in Jenkins
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
                        sh 'mvn -B -DskipTests clean package'  // Runs Maven build on Linux/macOS
                    } else {
                        bat 'mvn -B -DskipTests clean package'  // Runs Maven build on Windows
                    }
                }
            }
        }
    }

    post {
        always {
            junit(
                allowEmptyResults: true,
                testResults: '**/target/surefire-reports/*.xml'  // Ensure test reports are correctly located
            )
        }
    }
}
