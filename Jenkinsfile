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
    agent {
        kubernetes {
            // Spesifikasi label untuk node di Kubernetes
            label 'my-kubernetes-label'
            // Template pod untuk menggunakan image Node.js
            defaultContainer 'nodejs'
            yaml """
                apiVersion: v1
                kind: Pod
                metadata:
                  labels:
                    some-label: some-label-value
                spec:
                  containers:
                  - name: nodejs
                    image: node:lts-buster-slim
                    ports:
                    - containerPort: 3000
                    command:
                    - cat
                    tty: true
                  restartPolicy: Never
            """
        }
    }
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                container('nodejs') {
                    // Perintah npm install
                    sh 'npm install'
                }
            }
        }
        stage('Test') {
            steps {
                container('nodejs') {
                    // Jalankan skrip test.sh di dalam kontainer
                    sh './jenkins/scripts/test.sh'
                }
            }
        }
        stage('Deliver') {
            steps {
                container('nodejs') {
                    // Jalankan skrip deliver.sh di dalam kontainer
                    sh './jenkins/scripts/deliver.sh'
                    input message: 'Finished using the web site? (Click "Proceed" to continue)'
                    // Jalankan skrip kill.sh di dalam kontainer
                    sh './jenkins/scripts/kill.sh'
                }
            }
        }
    }
}



