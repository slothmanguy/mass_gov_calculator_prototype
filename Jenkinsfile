node {
    stage('Checkout') {
        checkout scm
    }
    stage('Build') {
        sh 'npm install'
        sh 'npm install karma-cli'

    }
    stage('Tests') {
        sh 'npm test'
    }
}