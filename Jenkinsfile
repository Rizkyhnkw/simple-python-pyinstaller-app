node {

    stage('Build') {
        docker.image('python:3-alpine').inside {
            sh 'python3 -m venv venv && source venv/bin/activate && python -m py_compile sources/add2vals.py sources/calc.py'
        }
    }

    stage('Test') {
        docker.image('python:3-alpine').inside {
            sh '''
                python3 -m venv venv
                source venv/bin/activate
                pip install --no-cache-dir pytest
                pytest --verbose --junit-xml test-reports/results.xml sources/test_calc.py
            '''
            junit 'test-reports/results.xml'
        }
    }

    stage('Manual Approval') {
        input message: 'Lanjutkan ke tahap Deploy?', ok: 'Proceed'
    }

    stage('Deploy') {
        docker.image('python:3-alpine').inside {
            sh '''
                python3 -m venv venv
                source venv/bin/activate
                python sources/add2vals.py 7 7
                sleep 60
            '''
        }
    }
}
