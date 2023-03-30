node {
    withDockerContainer('maven:3.9.0-eclipse-temurin-11') {
        stage('Build') {
            checkout scm
            sh 'mvn -B -DskipTests clean package'
        }
    }
    withDockerContainer('maven:3.9.0-eclipse-temurin-11') {
        stage('Test') {
            checkout scm
            sh 'mvn test'
            junit 'target/surefire-reports/*.xml'
        }
    }
    withDockerContainer('maven:3.9.0-eclipse-temurin-11') {
        stage('Manual Approval') {
            input message: 'Lanjut ke tahap Deploy? (Klik "Proceed" untuk melanjutkan)'
        }
    }
    withDockerContainer('maven:3.9.0-eclipse-temurin-11') {
        stage('Deploy') {
            sh './jenkins/scripts/deliver.sh'
            echo $! > .pidfile
            echo 'Aplikasi akan berakhir dalam 1 menit'
            sh 'sleep 60'
            kill $(cat .pidfile)
        }
    }
}