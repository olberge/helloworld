node('master') {
    checkout scm

    stage('scm-compile') {
        withMaven(jdk: 'JDK 8', maven: 'Default maven') {
            sh 'mvn clean compile'
        }
    }

    stage('scm-test') {
        withMaven(jdk: 'JDK 8', maven: 'Default maven') {
            sh 'mvn test'
        }
    }
}
