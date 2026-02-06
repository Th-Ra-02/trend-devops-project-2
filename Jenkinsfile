pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "thra21/guvi-project-repo:trend-web"
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Th-Ra-02/trend-devops-project-2.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }
        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                    echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                    docker push $DOCKER_IMAGE
                    '''
                }
            }
        }
        stage('Deploy to EKS') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'aws-eks-creds',
                    usernameVariable: 'AWS_ACCESS_KEY_ID',
                    passwordVariable: 'AWS_SECRET_ACCESS_KEY'
                )]) {
                    sh '''
                    
                    AWS_ACCESS_KEY_ID=$(echo "$AWS_ACCESS_KEY_ID" | tr -d " ")
                    AWS_SECRET_ACCESS_KEY=$(echo "$AWS_SECRET_ACCESS_KEY" | tr -d " ")
                    export AWS_ACCESS_KEY_ID
                    export AWS_SECRET_ACCESS_KEY
                    export AWS_DEFAULT_REGION=ap-south-1
                    
                    echo "Access Key (first 10 chars): ${AWS_ACCESS_KEY_ID:0:10}"
                    aws sts get-caller-identity
                    
                    aws eks update-kubeconfig --region ap-south-1 --name trend-eks
                    kubectl apply -f k8s/ --validate=false
                    kubectl rollout status deployment/trend-web --timeout=300s
                    kubectl get pods,svc
                    '''
                }
            }
        }
    }
}
