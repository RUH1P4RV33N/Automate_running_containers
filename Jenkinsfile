pipeline {
    agent any 

    stages {
        stage('Build') {
            steps {
                script {
                    bat 'docker login -u ruhi004 -p Ruhi@2004'

                    // Build and push Docker image
                    bat 'docker build -t w9-dd-app:latest .'
                    bat 'docker tag w9-dd-app:latest ruhi004/w9-dh-app:latest'
                    bat 'docker push ruhi004/w9-dh-app:latest'
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    echo 'Running tests...'
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    bat 'minikube start'
                    bat 'kubectl apply -f my-kube1-deployment.yaml'
                    bat 'kubectl apply -f my-kube1-service.yaml'
                    echo '✅ Deployed successfully to Minikube!'
                }
            }
        }
    }
}

//  minikube delete --all --purge
//  minikube start --driver=docker
//     minikube status
//     kubectl apply -f my-kube1-deployment.yaml 
//     kubectl apply -f my-kube1-service.yaml
//     minikube dashboard --url
//     kubectl get pods
//     kubectl get service