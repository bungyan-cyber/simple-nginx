pipeline {
    agent any
    environment {
        KUBE_CONFIG = credentials('minikube-kubeconfig')
    }
    stages {
        stage('Prepare .kube Directory') {
            steps {
                script {
                    sh 'mkdir -p /var/lib/jenkins/.kube'
                    sh 'sudo chown -R jenkins:jenkins /var/lib/jenkins/.kube'
                }
            }
        }
        stage('Copy Minikube Certificates and Keys') {
            steps {
                script {
                    sh 'mkdir -p /var/lib/jenkins/.minikube/profiles/minikube'
                    sh 'sudo cp /root/.minikube/ca.crt /var/lib/jenkins/.minikube/'
                    sh 'sudo cp -r /root/.minikube/profiles/minikube /var/lib/jenkins/.minikube/profiles/'
                    sh 'sudo chown -R jenkins:jenkins /var/lib/jenkins/.minikube'
                    sh 'chmod 600 /var/lib/jenkins/.minikube/ca.crt /var/lib/jenkins/.minikube/profiles/minikube/client.crt /var/lib/jenkins/.minikube/profiles/minikube/client.key'
                }
            }
        }
        stage('Copy kubeconfig') {
            steps {
                withCredentials([file(credentialsId: 'minikube-kubeconfig', variable: 'KUBE_CONFIG_PATH')]) {
                    script {
                        sh 'cp $KUBE_CONFIG_PATH /var/lib/jenkins/.kube/config'
                        sh "sed -i 's|/root/.minikube|/var/lib/jenkins/.minikube|g' /var/lib/jenkins/.kube/config"
                        sh 'chown jenkins:jenkins /var/lib/jenkins/.kube/config'
                        sh 'chmod 600 /var/lib/jenkins/.kube/config'
                    }
                }
            }
        }
        stage('Copy YAML Files') {
            steps {
                script {
                    // Update this path to the actual location of your YAML files
                    sh 'cp /home/simple-nginx/nginx-deployment.yaml /var/lib/jenkins/workspace/nginx-deployment/'
                    sh 'cp /home/simple-nginx/nginx-service.yaml /var/lib/jenkins/workspace/nginx-deployment/'
                }
            }
        }
        stage('Deploy to Minikube') {
            steps {
                script {
                    sh 'kubectl --kubeconfig=/var/lib/jenkins/.kube/config apply -f /var/lib/jenkins/workspace/nginx-deployment/nginx-deployment.yaml -f /var/lib/jenkins/workspace/nginx-deployment/nginx-service.yaml'
                }
            }
        }
    }
}
