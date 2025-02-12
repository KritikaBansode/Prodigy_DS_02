pipeline {
    agent any  // Runs on any available Jenkins agent

    tools {
        maven 'MAVEN'  // Ensure 'MAVEN' is exactly as configured in Jenkins
        jdk 'JDK'      // Ensure 'JDK' matches Jenkins configuration
    }

    stages {
        stage('Initialize') {
            steps {
                echo "Setting up environment variables"
                echo "PATH = ${M2_HOME}/bin:${PATH}"
                echo "M2_HOME = /opt/maven"
            }
        }

        stage('Check Java Version') {  // Added Java check stage
            steps {
                sh 'java -version'  // Ensures Java is correctly installed
            }
        }

        stage('Build') {
            steps {
                dir("/var/lib/jenkins/workspace/Java-Maven-Pipeline/my-app") {  
                    sh 'mvn -B -DskipTests clean package'  
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
