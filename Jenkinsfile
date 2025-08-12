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
        stage('Build Python Package') {
            steps {
                bat 'python -m pip install --upgrade pip setuptools wheel'
                bat 'python application/setup.py sdist bdist_wheel'
            }
        }
        stage('Upload to Artifactory') {
            steps {
                bat """
                    curl -u%JFROG_USER%:%JFROG_PASSWORD% ^
                    -T application/calculator.py ^
                    https://trialz1pw0e.jfrog.io/artifactory/test-generic-local/application/calculator.py
                """
            }
        }
        stage('archive artifacts') {
            steps {
                archiveArtifacts artifacts: 'application.zip', fingerprint: true
            }
        }
    }
}

