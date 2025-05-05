pipeline {
    agent any  // Runs on any available agent

    tools {
        maven 'Maven 3.9.1'   // Replace with the name of your Maven tool configured in Jenkins
        jdk 'JDK 17'          // Replace with your configured JDK name
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code...'
                checkout scm  // Gets code from the Git repo this Jenkins job is linked to
            }
        }

        stage('Build') {
            steps {
                echo 'Compiling the code...'
                bat 'mvn clean compile'  // Windows batch command
            }
        }

        stage('Test') {
            steps {
                echo 'Running unit tests...'
                bat 'mvn test'  // Windows batch command
            }

            post {
                always {
                    junit '**/target/surefire-reports/*.xml'  // JUnit report path
                }
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging the application...'
                bat 'mvn package'  // Windows batch command
            }
        }
    }

    post {
        success {
            echo 'Build and tests succeeded!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
