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
        sh 'python -m py_compile sources/add2vals.py sources/calc.py'
      }
    }
    stage('Test') {
      parallel {
        stage('Test') {
          agent {
            docker {
              image 'qnib/pytest'
            }

          }
          post {
            always {
              junit 'test-reports/results.xml'

            }

          }
          steps {
            sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
            junit 'test-reports/results.xml'
          }
        }
        stage('') {
          steps {
            junit 'test-reports/results.xml'
          }
        }
      }
    }
  }
}