// Jenkinsfile (Declarative Pipeline)

pipeline {
    // 1. Agent: 사용 가능한 모든 Agent(Controller 포함)에서 실행
    agent any

    // 2. Stages: 파이프라인의 주요 단계
    stages {
        stage('Code Checkout') {
            steps {
                echo 'Code successfully checked out.'
                // 이 단계에서 일반적으로 'checkout scm'이 자동으로 실행되거나 명시적으로 추가됩니다.
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                script {
                    // Jenkins Workspace 내의 'ansible' 폴더로 이동
                    dir('ansible') {
                        // Ansible Playbook 실행
                        sh 'ansible-playbook -i inventory.ini site.yml'
                    }
                }
            }
        }

        stage('Cleanup') {
            steps {
                echo 'Deployment finished.'
            }
        }
    }

    // 3. Post: 파이프라인 실행 후 처리
    post {
        always {
            // 모든 경우에 워크스페이스 정리
            deleteDir()
        }
        success {
            echo 'Ansible Deployment succeeded!'
        }
        failure {
            echo 'Ansible Deployment failed! Check logs.'
        }
    }
}
