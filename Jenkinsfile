    pipeline {
        agent {
            docker {
                image 'python:3.9-slim'
            }
        }
        stages {
            stage('Install Dependencies') {
                steps {
                    sh 'pip install --upgrade --user pip'
                }
            }
        }
    }
