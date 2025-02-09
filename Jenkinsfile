node {
    def pythonImage = 'python:3-alpine' 

    stage('Build') {
        docker.image(pythonImage).inside {
            sh 'pip install -r requirements.txt'
        }
    }

    stage('Test') {
        docker.image(pythonImage).inside {
            sh 'pip install pytest'
            sh 'pytest --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
        }
        junit 'test-reports/results.xml'
    }

    stage('Manual Approval') {
        input message: 'Lanjutkan ke tahap Deploy?', ok: 'Proceed'
    }

    stage('Deploy') {
        docker.image(pythonImage).inside {
            sh 'python sources/add2vals.py 7 7'
        }
    }
}
