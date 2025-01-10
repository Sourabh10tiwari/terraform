# terraform
Terraform practice repository

#Code to add in Jenkins pipeline in Jenkins server

pipeline {
    agent any
    
    environment {
        AWS_ACCESS_KEY_ID = credentials('aws-terraform')
        AWS_SECRET_ACCESS_KEY = credentials('aws-terraform')
    }
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', credentialsId: 'Git', url: 'https://github.com/Sourabh10tiwari/terraform'
            }
        }
        stage('Terraform init') {
            steps {
                sh 'terraform init'
            }
        }
        stage('Terraform Plan') {
            steps {
                script {
                    sh 'terraform plan -out=tfplan'
                }
            }
        }
        stage('Terraform apply') {
            steps {
                sh 'terraform apply --auto-approve'
            }
        }
        
    }
}
