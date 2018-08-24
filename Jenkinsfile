pipeline {
    agent {
        docker {
            image 'talabu/seltest:latest'
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package -DproxySet=true -DproxyHost=web-proxy.corp.hpecorp.net -DproxyPort=8080'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test -DproxySet=true -DproxyHost=web-proxy.corp.hpecorp.net -DproxyPort=8080'
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
