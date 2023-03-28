node {
    try {
        docker.image('maven:3-alpine').inside('-v /root/.m2:/root/.m2')
        stage('Build') {
            sh 'mvn -B -DskipTests clean package'
        }
        stage('Test') {
            sh 'mvn test'
            junit 'target/surefire-reports/*.xml'
        }
        slackSend color: 'good', message: "$JOB_NAME - Successfully built #$BUILD_NUMBER (<$BUILD_URL|Open>)"
    } catch (err) {
        slackSend color: 'danger', message: "$JOB_NAME - Failed #$BUILD_NUMBER (<$BUILD_URL|Open>)"
        throw(err)
    }
}