#!groovy
pipeline {
    agent {
        node {
            label 'master'
        }
    }
	environment {
	    AWS_ACCESS_KEY_ID = credentials('jenkins-aws-access-key')
        AWS_SECRET_KEY_ID = credentials('jenkins-aws-secret-key')
        TF_IN_AUTOMATION = '1'
    }
    stages {
        stage('git-checkout') {
            steps {
                sh 'rm -rf *;git clone https://github.com/onaiv22/terraform-jenkins-aws.git'
            }
        }
        stage('output terraform version') {
            steps {
                sh 'terraform --version'
            }
        }
        stage('cd into jenkins workspace for this project') {
            steps {
                sh 'cd /var/lib/jenkins/workspace/jenkins-node-aws-terraform/terraform-jenkins-aws'
            }
        }
        stage('copy terraform tfvars from homedir to workspace') {
            steps {
                sh 'sudo cp /root/terraform.tfvars /var/lib/jenkins/workspace/jenkins-node-aws-terraform/terraform-jenkins-aws/'
            }
        }
        
        stage('terraform init') {
            steps {
                sh 'terraform init -input=false'
            }
        }
        stage('terraform plan') {
            steps {
                sh 'terraform plan -input=false -out=tfplan.out'
            }
        }

    }
}
