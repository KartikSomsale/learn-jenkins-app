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
                bat 'echo "building images"'
            }
        }

        stage('AWS1'){
            agent any
            steps{
                docker{
                    image 'amazon/aws-cli'
                }
                withCredentials([usernamePassword(credentialsId: 'my-aws', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')]) {
                    // bat "docker run --rm -e AWS_ACCESS_KEY_ID=%AWS_ACCESS_KEY_ID% -e AWS_SECRET_ACCESS_KEY=%AWS_SECRET_ACCESS_KEY% amazon/aws-cli s3 ls"
                    // bat "docker run --rm amazon/aws-cli s3 ls"
                    sh '''
                        aws --version
                        aws s3 ls
                    '''
                }
                
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
                // bat 'netlify deploy --dir=build --json'
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
                // bat 'netlify deploy --dir=build --prod'
            }
        }
    }
}
