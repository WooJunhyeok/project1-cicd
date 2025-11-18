pipeline {
    agent any

    options {
        skipDefaultCheckout(true)
    }

    environment {
        SLACK_WEBHOOK = credentials('slack-webhook')   // Jenkins Credentials ID
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'master',
                    credentialsId: 'github-key',
                    url: 'git@github.com:WooJunhyeok/project1-cicd.git'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                cd ansible
                ansible-playbook -i inventory.ini site.yml
                '''
            }
        }
    }

    post {
        success {
            sh """
            curl -X POST -H 'Content-type: application/json' \
            --data '{\"text\":\"🎉 Jenkins Build SUCCESS - project1-cicd\"}' \
            $SLACK_WEBHOOK
            """
        }

        failure {
            sh """
            curl -X POST -H 'Content-type: application/json' \
            --data '{\"text\":\"❌ Jenkins Build FAILED - project1-cicd\"}' \
            $SLACK_WEBHOOK
            """
        }
    }
}

