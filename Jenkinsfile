pipeline{
    agent any
    stages {
        stage('Build'){
            steps {
                bat 'node --version'
                bat 'npm --version'
                bat 'npm ci'
                bat 'npm run build'
            }
        }
    }
}
