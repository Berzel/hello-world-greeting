pipeline {
    agent { node { label 'master' } }

    stages {

        stage ('Build') {
            steps {
                sh 'mvn clean install'
                archiveArtifacts 'target/**/*.war'
            }
        }

        stage ('Unit Testing') {
            steps {
                sh 'mvn clean verify -DskipITs=true';
                junit '**/target/surefire-reports/TEST-*.xml'
            }
        }

        stage ('Static Code Analysis') {
            steps {
                sh 'sonar-scanner -Dsonar.projectKey=example-project -Dsonar.sources=. -Dsonar.java.binaries=./target/'
            }
        }

        stage ('Integration Testing') {
            steps {
                sh 'echo "Running integration tests.."'
            }
        }

        stage('Artifactory: Publish') {
            steps {
                // rtUpload (
                //     serverId: 'Default Artifactory Server',
                //     spec: '''{
                //         "files": [
                //             {
                //             "pattern": "target/hello*.war",
                //             "target": "example-repo/${BUILD_NUMBER}/"
                //             }
                //         ]
                //     }''',
                // )
                sh 'echo "Publishing to artifactory..."'
            }
        }

        stage ('Deploy') {
            steps {
                sh 'echo "Deploying to staging.."'
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