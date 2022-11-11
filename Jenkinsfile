pipeline {  
    agent any

    environment{
        ENV_URL  = "pipeline.google.com"
        SSH_CRED = credentials('SSH')
    }

    stages {

        stage('Perform Lkint-checks') { // runs only when its a Feature branch
            steps {
                sh "env"
                sh "echo Performing Lint Checks"
            }
        }
        stage('Do a DRY-RUN') { // Runs only when its a PR
            steps {
                sh "ansible-playbook robot-dryrun.yml -e COMPONENT=mongodb -e ENV=dev -e ansible_user=${SSH_CRED_USR} -e ansible_password=${SSH_CRED_PSW}"
            }
        }
        stage('main') {               // Runs only when its a main branch
            when { branch 'main' }
            steps {
                sh "env"
                sh "echo I am a Main Branch"
            }
        }
    }
}