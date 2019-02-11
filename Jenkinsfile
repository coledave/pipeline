
def awesomeVersion = '18.10'

pipeline {
  agent {
    kubernetes {
      label 'area1'
      yaml """
apiVersion: v1
kind: Pod
spec:
  containers:
    - name: ubuntu
      image: ubuntu:${awesomeVersion}
      command:
        - cat
      tty: true
"""
    }
  }
  stages {
    stage('Hello World - Area 1') {
      steps {
        script {
            commitId = sh(returnStdout: true, script: 'git rev-parse HEAD')
            print commitId
        }  
        sh 'pwd'
        sh 'cat /etc/*release'
      }
    }
    stage('Hello World - Area 2') {
      agent {
        kubernetes {
          label 'area2'
          yaml """
apiVersion: v1
kind: Pod
spec:
  containers:
    - name: ubuntu
      image: ubuntu:${commitId}
      command:
        - cat
      tty: true
"""
        }
      }
      steps {
        container ('ubuntu') {
          sh 'pwd'
          sh 'cat /etc/*release'
        }
      }
    }
  }
}
