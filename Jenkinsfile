pipeline {
    agent any

    triggers {
        githubPush()
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
                sudo -u ansible bash -lc '
                    cd /opt/infra/ansible && \
                    ansible-playbook -i inventory.ini site.yml
                '
            '''
        }
    }

    }

    post {
        success {
            echo 'Ansible playbook executed successfully.'
        }
        failure {
            echo 'Ansible playbook failed. Check logs.'
        }
    }
}

