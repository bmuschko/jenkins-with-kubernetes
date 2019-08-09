pipeline {
    agent {
        kubernetes {
            defaultContainer 'jnlp'
            yaml """
apiVersion: v1
kind: Pod
metadata:
  labels:
    some-label: some-label-value
spec:
  containers:
  - name: maven
    image: maven:alpine
    command:
    - cat
    tty: true
  - name: busybox
    image: busybox
    command:
    - cat
    tty: true
"""
        }
    }
    stages {
        stage('Run in Maven container') {
            steps {
                container('maven') {
                    sh 'mvn -version'
                }
            }
        }
        stage('Run in Busybox container') {
            steps {
                container('busybox') {
                    sh '/bin/busybox'
                }
            }
        }
        stage('Run in default container') {
            steps {
                sh "echo 'Running in default container'"
            }
        }
    }
}