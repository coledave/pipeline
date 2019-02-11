pipeline {
  agent {
    kubernetes {
      label 'mypod'
      defaultContainer 'jnlp'
      yaml """
apiVersion: v1
kind: Pod
metadata:
  labels:
    some-label: some-label-value
spec:
  containers:
    - name: ubuntu
      image: ubuntu:18.04
      command:
        - cat
      tty: true
"""
    }
  }
  stages {
    stage('Hello World') {
      steps {
        container('ubuntu') {
          sh 'cat /etc/*release'
        }
      }
    }
  }
}
