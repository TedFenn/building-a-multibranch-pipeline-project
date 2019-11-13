pipeline {
    agent {
        kubernetes {
        label 'regular-pod'
        yaml '''
            apiVersion: v1
            kind: Pod
            spec:
              containers:
                - name: apline
                  image: node:6-alpine
                  command:
                  - cat
                  tty: true
            '''
        }
    }
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                container(name: 'regular-pod')
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                container(name: 'regular-pod')
                sh './jenkins/scripts/test.sh'
            }
        }
    }
}
