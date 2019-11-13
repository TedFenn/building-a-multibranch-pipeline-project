pipeline {
    agent {
        kubernetes {
        label 'regular-pod'
        yamlFile 'test.yaml'
        }
    }
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                container(name: 'alpine') {
                    sh 'npm install'
                }
            }
        }
        stage('Test') {
            steps {
                container(name: 'alpine') {
                    sh './jenkins/scripts/test.sh'
                }
            }
        }
        stage('Deliver for development') {
            when {
                branch 'development'
            }
            steps {
                sh './jenkins/scripts/deliver-for-development.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
        stage('Deploy for production') {
            when {
                branch 'production'
            }
            steps {
                sh './jenkins/scripts/deploy-for-production.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
