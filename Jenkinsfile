pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Verify PHP') {
            steps {
                sh 'php -v'
                sh 'phpunit --version'
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh 'phpunit tests'
            }
        }

        stage('Use Secret') {
            steps {
                withCredentials([string(credentialsId: 'github-token', variable: 'GITHUB_TOKEN')]) {
                    sh 'echo "GitHub token loaded securely"'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline Finished'
        }

        success {
            echo 'All tests passed successfully'
        }

        failure {
            echo 'Tests failed'
        }
    }
}
