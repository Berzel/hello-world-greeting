pipeline {
    agent { node { label 'docker' } }

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
                sh 'mvn sonar:sonar -Dsonar.projectKey=example-project -Dsonar.host.url=http://localhost:9000 -Dsonar.projectVersion=$BUILD_NUMBER -Dsonar.login=sonarqube'
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