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
                        withMaven(jdk: 'JDK 8', maven: 'Default maven') {
                    		    sh 'mvn test'
                        }
                    }
                }
                stage('Test Branch B') {
                    steps {
                        sh 'sleep 15s'
                    }
                }
                stage('Test Branch C') {
	                  /* agent { label 'ecs-agent' } */
                    steps {
                        sh 'sleep 10s'
                    }
                }
            }

        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                withMaven(jdk: 'JDK 8', maven: 'Default maven') {
                    sh 'mvn install'
                }
            }
        }
    }
    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}
