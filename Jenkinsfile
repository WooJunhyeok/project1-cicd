pipeline {
    agent any

    options {
        skipDefaultCheckout(true)
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-key',
                    url: 'git@github.com:WooJunhyeok/project1-cicd.git'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                ansible-playbook -i /etc/ansible/hosts /etc/ansible/deploy.yml
                '''
            }
        }
    }
}

