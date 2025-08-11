pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(
                    branches: [[name: '*/main']],
                    extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'application']],
                    userRemoteConfigs: [[url: 'https://github.com/AjayKumar9375/ci-cd_demo.git']]
                )
            }
        }
        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }


        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }
        stage('App') {
            steps {
                catchError(buildResult: 'UNSTABLE', stageResult: 'FAILURE') {
                    echo "Running tests on branch: ${env.BRANCH_NAME}"
                    bat 'python application/calculator.py'
                }
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying branch: ${env.BRANCH_NAME}"
            }
        }
    }
}

