pipeline {
  agent {
    kubernetes {
      label 'mypod'
      yaml """
apiVersion: v1
kind: Pod
spec:
  containers:
    - name: ubuntu1804
      image: ubuntu:18.04
      command:
        - cat
      tty: true
    - name: ubuntu1810
      image: ubuntu:18.10
      command:
        - cat
      tty: true
"""
    }
  }
  stages {
    stage('Hello World') {
      steps {
        sh 'pwd'
        sh 'cat /etc/*release'
      }
    }
  }
}
