pipeline {
    agent none
    stages {
        stage('Build') {
            agent {
                docker {
                    image 'python:2-alpine'
                }
            }
            steps {
                sh 'python -m pip install -r src/requirements.txt'
                sh 'python -m py_compile src/add2vals.py src/calc.py'
            }
        }
        stage('Test') {
            agent {
                docker {
                    image 'qnib/pytest'
                }
            }
            steps {
                sh 'python -m pip install -r src/requirements.txt'
                sh 'py.test --verbose --junit-xml test-reports/results.xml src/test_calc.py'
            }
            post {
                always {
                    junit 'test-reports/results.xml'
                }
            }
        }
    }
}
