pipeline {
    agent { docker { image 'maven:3.3.3' } }
    stages {
        stage('build') {
            steps {
                sh 'mvn -B -DskipTests clean install -DproxySet=true -DproxyHost=web-proxy.corp.hpecorp.net -DproxyPort=8080'
            }
        }
    }
}
