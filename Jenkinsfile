node {
    withDockerContainer(args: '-v /root/.m2:/root/.m2 --network host', image: 'maven:3.9.0') {
        stage('Build') {
            checkout scm
            script {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            checkout scm
            script {
                sh 'mvn test'
            }
            junit 'target/surefire-reports/*.xml'
        }
        stage('Deploy') {
            checkout scm
            script {
                sh './jenkins/scripts/deliver.sh'
            }
            sleep time: 1, unit: 'MINUTES'
        }
    }
}