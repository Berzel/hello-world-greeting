pipeline {
    agent { node { label 'master' } }

    stages {
        stage ('Build & Unit Test') {
            steps {
                sh 'mvn clean verify -DskipITs=true';
                junit '**/target/surefire-reports/TEST-*.xml'
                archive 'target/*.jar'
            }
        }

        stage ('Static Code Analysis') {
            steps {
                sh 'sonar-scanner -Dsonar.projectKey=example-project -Dsonar.sources=. -Dsonar.java.binaries=./target/ -Dsonar.host.url=http://localhost:9000 -Dsonar.sourceEncoding=UTF-8'
            }
        }

        stage ('Integration Testing') {
            steps {
                sh 'echo "Running integration tests.."'
            }
        }

        stage ('Deploy') {
            steps {
                sh 'echo "Deploying.."'
            }
        }
    }


    post {
        always {
            echo 'This will always run after a build whether it was successful or not'
        }

        success {
            echo 'This will only execute if the pipeline completed successfully'
        }

        failure {
            echo 'This will only run if the pipeline fails' // Pipeline failure happens when exit code of command is non zero
        }

        unstable {
            echo 'This will only run if the run was marked as unstable' // A pipeline that has failing tests will be marked as unstable
        }

        changed {
            echo 'This will only run if the state of the pipeline has changed' // State may change from failure to success
        }
    }
}