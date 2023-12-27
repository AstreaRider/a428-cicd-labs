// pipeline {
//     agent any
//     stages {
//         stage('Build') { 
//             agent {
//                 kubernetes {
//                     image 'node:lts-buster-slim'
//                 }
//             }
//             steps {
//                 sh 'npm install' 
//             }
//         }
//         stage('Test') {
//             steps {
//                 sh './jenkins/scripts/test.sh'
//             }
//         }
//         stage('Deploy') {
//             steps {
//                 sh './jenkins/scripts/deliver.sh'
//                 input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)'
//                 sh './jenkins/scripts/kill.sh'
//             }
//         }
//     }
// }

pipeline {
    podTemplate(containers: [
    containerTemplate(
        name: 'node', 
        image: 'node:lts-buster-slim'
        )
  ]) {

    node(POD_LABEL) {
        stage('React App CI') {
            container('node') {
                stage('Build') {
                    sh 'npm install'
                }
            }
        }

    }
}
}

