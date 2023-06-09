node {
    withDockerContainer(args: '-p 3000:3000', image: 'node:16-buster-slim') {
        stage('Build'){
            sh 'npm install'
        }
        stage('test'){
            sh './jenkins/scripts/test.sh'
        }
    }
}