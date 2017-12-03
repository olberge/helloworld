pipeline {
    agent { label 'ecs-agent' }
    stages {
        stage('Build') {
            steps {
		withMaven(jdk: 'JDK 8', maven: 'Default maven') {
                    sh 'mvn clean compile'
		}
            }
        }
        stage('Test') {
            failFast true
            parallel {
                stage('Test Branch A') {
                    steps {
                        sh 'mvn test'
                    }
                }
                stage('Branch B') {
                    steps {
                        sh 'mvn test'
                    }
                }
            }

        }
        stage('Deploy') {
            agent { label 'ecs-agent' }
            steps {
                echo 'Deploying....'
                sh 'mvn install'
            }
        }
    }
}

