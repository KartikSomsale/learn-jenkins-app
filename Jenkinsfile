pipeline{
    agent any
    stages {
        /*stage('Build'){
            steps {
                bat 'echo node --version'
                bat 'npm ci'
                bat 'npm run build'
            }
        }

        stage('Test'){
            steps{
                bat 'echo "Testing..."'
                bat 'npm test'
            }
        }*/

        stage('E2E'){
            agent{
                docker{
                    image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
                    args '-u root:root'
                }
            }
            steps{
                bat 'npm install -g serve'
                bat 'node_modules/serve -s build'
                bat 'npx playwright test'
            }
        }

        stage('Deploy'){
            steps{
                bat 'npm install netlify-cli -g'
                bat 'netlify --version'
            }
        }
    }
}
