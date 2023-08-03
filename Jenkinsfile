#!/usr/bin/env groovy
pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID = credentials('AKIASPBWESJLMSUYIBFI') 
        AWS_SECRET_ACCESS_KEY = credentials('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')
        AWS_DEFAULT_REGION = "us-east-2"
    }
    stages {
        stage("Create an EKS Cluster") {
            steps {
                script {
                    dir('Terraform') {
                        sh "terraform init -upgrade"
                        sh "terraform apply --auto-approve"
                    }
                }
            }
        }
        stage("Deploy to EKS") {
            steps {
                script {
                    dir('Kubernetes') {
                        sh "aws eks update-kubeconfig --name myapp-eks-cluster"
                        sh "kubectl apply -f nginx-deployment.yaml"
                        sh "kubectl apply -f nginx-service.yaml"
                    }
                }
            }
        }
    }
}
