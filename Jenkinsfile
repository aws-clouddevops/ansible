pipeline {  
    agent any

    environment {
        ENV_URL  = "pipeline.google.com"
        SSH_CRED = credentials('SSH')
    }

    stages {
        stage('Perform Lint-checks') { // runs only when its a Feature branch
            when { branch pattern: "feature-.*", comparator: "REGEXP" }
            steps {
                sh "env"
                sh "echo Performing Lint Checks"
            }
        }
        stage('Do a DRY-RUN') { // Runs only when its a PR
             when { branch pattern: "PR-.*", comparator: "REGEXP" }
             steps {
                sh "ansible-playbook robot-dryrun.yml -e COMPONENT=mongodb -e ENV=dev -e ansible_user=${SSH_CRED_USR} -e ansible_password=${SSH_CRED_PSW}"
            }
        }
        stage('main') {               // Runs only when its a main branch
            when { expression {env.TAG_NAME != null} } // We are checking whether the value of TAG_NAME is null or not
            steps {
                sh "env"
                sh "echo I am a Main Branch"
            }
        }
    }
}

// TAG_NAME Variable only comes up when you run it again the TAG_NAME rest of thr times. it wont be there