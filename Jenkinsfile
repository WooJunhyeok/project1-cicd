pipeline {
    agent any

    options {
        skipDefaultCheckout(true)
    }

    environment {
        SLACK_WEBHOOK = credentials('slack-webhook')
        ANSIBLE_HOST_KEY_CHECKING = 'False'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'master',
                    credentialsId: 'github-key',
                    url: 'git@github.com:WooJunhyeok/project1-cicd.git'
            }
        }

        stage('Deploy All (DNS + Monitoring + Jenkins)') {
            steps {
                sh '''
                cd ansible
                ansible-playbook -i inventory.ini site.yml \
                --extra-vars "slack_webhook_url=$SLACK_WEBHOOK slack_channel=#alerts"
                '''
            }
        }
/*
        stage('Deploy Load Balancer') {
            steps {
                sh '''
                cd ansible
                ansible-playbook -i inventory.ini playbook/lb-deploy.yml
                '''
            }
        }
*/
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

