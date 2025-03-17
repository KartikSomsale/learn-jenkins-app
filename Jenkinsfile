pipeline{
    agent any

    environment{
        NETLIFY_SITE_ID = "e82ef68d-6c73-4092-a1f4-0a3c3645ff04"
        NETLIFY_AUTH_TOKEN = credentials('netlify-token')
    }
    stages {
        stage('docker'){
            steps{
                // bat 'docker build . -t my-playwright'
                bat 'echo "building image"'
            }
        }

        stage('AWS'){
            agent{
                docker{
                    image 'amazon/aws-cli'
                }
            }
            steps{
                bat 'aws --version'
            }
        }
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

        stage('Deploy Staging'){
            steps{
                // bat 'npm install netlify-cli'
                // bat 'node_modules/.bin/netlify --version'
                bat 'echo "Deploying into Staging, Site ID : "%NETLIFY_SITE_ID%'
                bat 'netlify deploy --dir=build --json'
            }
        }
        stage('Approval'){
            steps{
                timeout(1) {
                    input cancel: 'No', message: 'Do you want to Deploy into Production', ok: 'Yes, I am sure.'
                }
            }
        }
        stage('Deploy Prod'){
            steps{
                // bat 'npm install netlify-cli'
                // bat 'node_modules/.bin/netlify --version'
                bat 'echo "Deploying into Production, Site ID : "%NETLIFY_SITE_ID%'
                bat 'netlify deploy --dir=build --prod'
            }
        }
    }
}
