git remote add origin https://github.com/avelmuruganofficials-sudo/git-practice7111.gitpipeline {
 pipeline {
    agent any

    tools {
        nodejs 'node18'
    }

    triggers {
        cron('H 2 * * *')   // Runs daily at ~2 AM
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/<your-username>/<your-repo>.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                npm install
                npx playwright install
                '''
            }
        }

        stage('Run Playwright Tests') {
            steps {
                sh '''
                npx playwright test
                '''
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'playwright-report/**', fingerprint: true
        }

        success {
            emailext(
                subject: "✅ Playwright Tests Passed - Landydev",
                body: "All Playwright tests passed successfully.",
                to: "yourmail@gmail.com"
            )
        }

        failure {
            emailext(
                subject: "❌ Playwright Tests Failed - Landydev",
                body: "Tests failed. Please check Jenkins console logs.",
                to: "yourmail@gmail.com"
            )
        }
    }
}


