pipeline {
    agent {
        docker {
            image 'python:3.9-slim' 
            args '-p 3000:3000'    
        }
    }
    stages {
        stage('Setup') { 
            steps {
                sh 'python -m venv venv' 
                sh '. venv/bin/activate && pip install --upgrade pip setuptools' 
                sh '. venv/bin/activate && pip install -r requirements.txt' 
            }
        }
        stage('Test') { 
            steps {
                sh '. venv/bin/activate && pytest tests/' 
            }
        }
    }
}
