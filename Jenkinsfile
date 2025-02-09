node {
    stage('Build') {
        docker.image('python:2-alpine').inside {
            sh 'python -m py_compile sources/add2vals.py sources/calc.py'
        }
    }
    
    stage('Test') {
        docker.image('qnib/pytest').inside {
            sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
        }
        
        // Post actions
        junit 'test-reports/results.xml'
    }
     stage('Manual Approval') {
            input message: 'Lanjutkan ke tahap Deploy?', ok: 'Proceed'
        }
      stage('Deploy') {
            sh './jenkins/scripts/deliver.sh'
            sh 'sleep 60'
            sh './jenkins/scripts/kill.sh'
        }
}
