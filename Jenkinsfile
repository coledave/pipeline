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
      image: ubuntu:18.04
      command:
        - cat
      tty: true
"""
    }
  }
  stages {
    stage('Hello World - Area 1') {
      steps {
        container ('ubuntu') {
          sh 'pwd'
          sh 'echo "Hello" > world.txt'
          sh 'cat /etc/*release'
        }
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
      image: ubuntu:18.10
      command:
        - cat
      tty: true
"""
        }
      }
      steps {
        container ('ubuntu') {
          sh 'pwd'
          sh 'ls -lah'
          sh 'cat /etc/*release'
        }
      }
    }
  }
}
