pipeline{
    agent any
    stages {
        stage('Build'){
            setps {
                bat 'echo node --version'
                bat 'npm ci'
                bat 'npm run build'
            }
        }
    }
}
