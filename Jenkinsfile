node {
    try {
        def mvnHome
        stage('Preparation') {
            git 'https://github.com/nndakurnia/simple-java-maven-app.git'           
            mvnHome = tool 'M3'
        }
        stage('Build') {
            sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
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