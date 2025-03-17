pipeline{
    agent any

    environment{
        NETLIFY_SITE_ID = "e82ef68d-6c73-4092-a1f4-0a3c3645ff04"
    }
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

        // stage('E2E'){
        //     agent{
        //         docker{
        //             image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
        //             args '-u root:root'
        //         }
        //     }
        //     steps{
        //         bat 'npm install -g serve'
        //         bat 'node_modules/serve -s build'
        //         bat 'npx playwright test'
        //     }
        // }

        stage('Deploy'){
            steps{
                // bat 'npm install netlify-cli'
                // bat 'node_modules/.bin/netlify --version'
                bat '$NETLIFY_SITE_ID'
            }
        }
    }
}
