node ('docker') {
     stage ('Build & Unit Test') {
        sh 'mvn clean verify -DskipITs=true';
        junit '**/target/surefire-reports/TEST-*.xml'
        archive 'target/*.jar'
    }

    stage ('Static Code Analysis') {
        sh 'mvn sonar:sonar -Dsonar.projectKey=example-project -Dsonar.host.url=http://localhost:9000 -Dsonar.projectVersion=$BUILD_NUMBER -Dsonar.login=sonarqube'
    }

    stage ('Integration Testing') {
        sh 'echo "Running integration tests.."'
    }

    stage ('Deploy') {
        sh 'echo "Deploying.."'
    }
}