node('master') {

    checkout scm

    stage('scm') {
        withMaven(jdk: 'JDK 8', maven: 'Default maven') {
            sh 'mvn clean install'
        }
    }
}

