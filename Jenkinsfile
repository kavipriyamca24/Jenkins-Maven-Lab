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
                bat 'mvn -B clean install'
            }
        }

        stage('Test Results') {
            steps {
                echo "Running unit tests..."
                junit '**/target/surefire-reports/*.xml'
            }
        }

        stage('Archive Artifacts') {
            steps {
                echo "Archiving built JAR files..."
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo '✅ Build SUCCESSFUL!'
        }
        failure {
            echo '❌ Build FAILED!'
        }
    }
}
