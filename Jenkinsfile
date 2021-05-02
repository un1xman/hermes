pipeline {
    agent { label 'master' }
    stages {
        stage('Execute Playbook') {
            steps {
                script {
                sh '''
                    ansible-playbook playbook.yaml -e KUBECONFIG="${KUBECONFIG}"
                '''
                }
            }
        }
    }
    post { always { cleanWs() } }
}