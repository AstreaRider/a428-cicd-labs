node {
    withDockerContainer(args: '-p 3000:3000', image: 'node:16-buster-slim') {
        stage('Build'){
            sh 'npm install'
        }
        stage('Test'){
            sh './jenkins/scripts/test.sh'
        }
        stage('Deploy'){
            timeout(time: 60, unit: 'SECONDS') {
                sh './jenkins/scripts/deliver.sh'
            }
            sh './jenkins/scripts/kill.sh'
        }
    }
}