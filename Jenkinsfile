pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/dev']], extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'application']], userRemoteConfigs: [[url: 'https://github.com/AjayKumar9375/ci-cd_demo.git']])
            }
        }
        stage('Build') {
            steps {
                echo "Building branch: ${env.BRANCH_NAME}"
            }
        }
        stage('Test') {
            steps {
                echo "Running tests on branch: ${env.BRANCH_NAME}"
                bat 'python application/calculator.py'
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying branch: ${env.BRANCH_NAME}"
            }
        }
    }
}
