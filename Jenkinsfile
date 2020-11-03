pipeline {
    agent { docker { image 'maven:3.3.3' } }
    environment {
    	DISABLE_AUTH = 'true'
    }

    stages {
        stage('build') {
            steps {
                sh 'mvn --version'
            }
        }

        stage('deploy') {
        	steps {
        		retry(3) {
                    sh './test.sh'
                }

                timeout(time: 3, unit: 'MINUTES') {
                    sh './health-check.sh'
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


