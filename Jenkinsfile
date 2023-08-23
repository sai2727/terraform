pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout your Git repository containing Terraform code
                git url: 'https://github.com/sai2727/terraform.git', credentialsId: 'aws-jenkins'
            }
        }

        stage('Terraform Init') {
            steps {
                // Initialize Terraform in the repository directory
                script {
                    sh "terraform init"
                }
            }
        }

         stage('Terraform Apply') {
  steps {
                // Use withCredentials to securely access AWS credentials
                withCredentials([string(credentialsId: 'aws-jenkins', variable: 'AWS_ACCESS_KEY_ID'),
                                 string(credentialsId: 'aws-jenkins', variable: 'AWS_SECRET_ACCESS_KEY')]) {
                    // Set AWS environment variables
                    withEnv(["AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY_ID}",
                             "AWS_SECRET_ACCESS_KEY=${AWS_SECRET_ACCESS_KEY}",
                             "AWS_DEFAULT_REGION=us-east-1"]) {
                        // Run Terraform apply
                        sh "terraform apply -auto-approve"
                    }
                }
            }
    }
    
    post {
        always {
            // Cleanup and destroy resources if the build fails
            script {
                // Run Terraform destroy to cleanup resources
                sh "terraform destroy -auto-approve"
            }
        }
    }
}
