pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
        AWS_DEFAULT_REGION = "us-east-1"
    }
  /*  stages {
        stage("Create EKS Cluster") {
            steps {
                script {
                    dir('terraform') {
                        sh "terraform init"
                        sh "terraform validate"
                        sh "terraform plan"
                        sh "terraform apply -auto-approve"
                    }
                }
            }
        }
        stage("Frontend Deployment to EKS") {
            steps {
                script {
                    dir('k8s_manifests/mongo') {
                        sh "aws eks update-kubeconfig --name my-eks-cluster --region us-east-1"
                        sh "kubectl create ns workshop"
                        sh "kubectl config set-context --current --namespace workshop"
                        sh "kubectl apply -f secrets.yaml"
                        sh "kubectl apply -f deploy.yaml"
                        sh "kubectl apply -f service.yaml"
                    }
                }
            }
        } */
        stage("Backend Deployment to EKS") {
            steps {
                script {
                    dir('k8s_manifests') {
                        sh "kubectl apply -f backend-deployment.yaml"
                        sh "kubectl apply -f backend-service.yaml"
                        sh "kubectl apply -f frontend-deployment.yaml"
                        sh "kubectl apply -f frontend-service.yaml"
                        sh "kubectl apply -f full_stack_lb.yaml"
                    }
                }
            }
        }
        /* stage("Delete EKS Frontend") {
            steps {
                script {
                    dir('k8s_manifests/mongo') {
                        sh "kubectl delete -f ."
                    }
                }
            }
        }
        stage("Delete Backend") {
            steps {
                script {
                    dir('k8s_manifests') {
                        sh "kubectl delete -f ."
                    }
                }
            }
        }
        stage("Delete EKS Cluster") {
            steps {
                script {
                    dir('terraform') {
                        sh "terraform destroy -auto-approve"
                    }
                }
            }
        } */
    }
}
