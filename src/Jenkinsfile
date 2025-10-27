pipeline {
    agent any

    tools {
        maven 'Maven_3'   // must match name in Jenkins Global Tool Configuration
        jdk 'JDK11'       // name of configured JDK in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo "Running mvn clean install"
                sh 'mvn -B clean install'
            }
        }

        stage('Test Results') {
            steps {
                // test results will be published in post/always
                echo "Testing finished — will publish results"
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true, allowEmptyArchive: true
            }
        }
    }

    post {
        always {
            junit '**/target/surefire-reports/*.xml'
        }
        success {
            echo 'Build SUCCESS'
        }
        failure {
            echo 'Build FAILED'
        }
    }
}
