node {
    stage('Build') {
        docker.image('python:3-alpine').inside {
            sh 'python3 -m compileall sources/add2vals.py sources/calc.py'
        }
    }

    stage('Test') {
        docker.image('python:3-alpine').inside {
            sh 'pip install --no-cache-dir pytest'  // Install pytest
            sh 'pytest --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
        }

        junit 'test-reports/results.xml'
    }

    stage('Manual Approval') {
        input message: 'Lanjutkan ke tahap Deploy?', ok: 'Proceed'
    }

    stage('Deploy') {
        docker.image('python:3-alpine').inside {
            sh 'python3 sources/add2vals.py 10 10'  // Gunakan python3
            sh 'sleep 60'
        }
    }
}
