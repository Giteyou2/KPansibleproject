pipeline {
    agent any

    triggers {
        githubPush()   // GitHub Webhook
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                sh '''
                cd playbooks
                ansible-playbook -i ../inventory/hosts deploy.yml
                '''
            }
        }
    }

    post {
        success {
            echo 'Ansible deployment completed successfully.'
        }
        failure {
            echo 'Deployment failed. Check the logs.'
        }
    }
}
