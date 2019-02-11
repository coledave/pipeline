
def awesomeVersion = '18.10'
def branch = BRANCH_NAME

print branch

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
      image: ubuntu:${branch}
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
          sh 'cat /etc/*release'
        }
      }
    }
    stage('Hello World - Area 2') {
      agent {
        kubernetes {
          label 'area2'
          yamlFile 'pod.yaml'
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
