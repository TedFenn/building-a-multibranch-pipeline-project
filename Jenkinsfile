pipeline {
    agent {
        docker {
            kubernetes {
             label 'regular-pod'
                yaml '''
                apiVersion: v1
                kind: Pod
                spec:
                  containers:
                    - name: node-alpine
                      image: node:6-alpine
                      command:
                      - cat
                      tty: true
                      EXPOSE 3000/tcp
                      EXPOSE 5000/tcp
                '''
        }
    }
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
    }
}
