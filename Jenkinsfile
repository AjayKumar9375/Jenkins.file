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
        stage('Build Python Package') {
            steps {
                bat 'pip install --upgrade pip setuptools wheel'
                bat 'python setup.py sdist bdist_wheel'
            }
        }
        stage('Upload to Artifactory') {
            steps {
                bat """
                    curl -u %JFROG_USER%:%JFROG_PASSWORD% ^
                    -T dist/my_app-1.0.0-py3-none-any.whl ^
                    https://trialz1pw0e.jfrog.io/artifactory/tf-trial/my_app-1.0.0-py3-none-any.whl
                """
            }
        }
    }
}

