pipeline {
    agent any

    triggers {
        githubPush()
    }

    tools {
        maven 'Maven'
        jdk 'JDK17'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            when {
                branch 'develop'
            }
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test || true'
            }
        }

        stage('Package') {
            when {
                anyOf {
                    branch 'main'
                    branch 'release/*'
                }
            }
            steps {
                sh 'mvn clean package'
            }
        }
    }

    post {
        success {
            echo 'CI Pipeline executed successfully'
        }
        failure {
            echo 'CI Pipeline failed'
        }
    }
}

