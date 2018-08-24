pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2 -e  http_proxy=http://web-proxy.corp.hpecorp.net:8080 -e https_proxy=http://web-proxy.corp.hpecorp.net:8080'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'echo hello in build'
            }
        }
        stage('Test') {
            steps {
                sh 'echo hello in test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
