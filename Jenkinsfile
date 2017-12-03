node('ecs-agent') {

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

    stage('run-parallel-branches') {
            parallel(
                a: {
                    echo "This is branch a"
                },
                b: {
                    echo "This is branch b"
                }
            )
    }

    stage('scm-install') {
        withMaven(jdk: 'JDK 8', maven: 'Default maven') {
            sh 'mvn install'
        }
    }
}
