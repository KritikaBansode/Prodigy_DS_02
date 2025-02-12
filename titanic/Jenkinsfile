pipeline {
    agent any  // Runs on any available Jenkins agent

    tools {
        maven "MAVEN" // Uses Maven installed in Jenkins
        jdk "JDK"     // Uses Java JDK installed in Jenkins
    }

    stages {
        stage('Initialize') {
            steps {
                echo "Setting up environment variables"
                echo "PATH = ${M2_HOME}/bin:${PATH}"
                echo "M2_HOME = /opt/maven"
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
