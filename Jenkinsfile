pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master',
                    credentialsId: 'github-key',
                    url: 'git@github.com:WooJunhyeok/project1-cicd.git'
            }
        }

        stage('Test') {
            steps {
                echo "Git pull 성공!"
            }
        }
    }
}

