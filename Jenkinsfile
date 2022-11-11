pipeline {  
    agent any

    environment{
        ENV_URL  = "pipeline.google.com"
        SSH_CRED = credentials('SSH')
    }
    stages {
        stage('Do a DRY-RUN') {
            steps {
                sh "ansible-playbook robot-dryrun.yml -e COMPONENT=mongodb -e ENV=dev -e ansible_user=${SSH_CRED_USR} -e ansible_password=${SSH_CRED_PSW}"
            }
        }
    }
}