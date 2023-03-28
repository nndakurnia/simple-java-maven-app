node {
    withDockerContainer('maven:3.9.0-eclipse-temurin-11') {
        // some block
        stage('Build') {
            checkout scm
            sh 'mvn -B -DskipTests clean package'
        }
    }
    withDockerContainer {
        // some block
        stage('Test') {
            checkout scm
            sh 'mvn test'
            junit 'target/surefire-reports/*.xml'
        }
    }
}