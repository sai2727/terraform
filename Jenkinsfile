pipeline {
    agent any

    tools {
        terraform 'terraform'
    }

    stages {
        stage ("checkout from GIT") {
            steps {
               git branch: 'feature', url:'https://github.com/sai2727/terraform.git'
            }
        }
        stage ("terraform init") {
            steps {
                sh 'terraform init'
            }
        }
        stage ("terraform fmt") {
            steps {
                sh 'terraform fmt'
            }
        }
        stage ("terraform validate") {
            steps {
                sh 'terraform validate'
            }
        }
        stage ("terrafrom plan") {
            steps {
                sh 'terraform plan '
            }
        }
        
        stage(action) {
            steps {
                echo "Terraform action is --> ${action}"
                sh ('terraform ${action} --auto-approve')
            }
        }
    }
}
