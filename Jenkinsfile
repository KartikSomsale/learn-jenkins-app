pipeline{
    agent any
    stages {
        stage('Build'){
            steps {
                bat 'echo node --version'
                bat 'npm ci'
                bat 'npm run build'
            }
        }
    }
}
