pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-key',
                    url: 'git@github.com:YOUR_ID/project-cicd.git'
            }
        }

        stage('Test') {
            steps {
                echo "Git pull 성공!"
            }
        }
    }
}
