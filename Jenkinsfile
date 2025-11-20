pipeline {
    agent any 

    stages {
        stage('Build') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                        bat "docker login -u %USER% -p %PASS%"
                    }

                    bat 'docker build -t w9-dd-app:latest .'
                    bat 'docker tag w9-dd-app:latest ruhi004/w9-dh-app:latest'
                    bat 'docker push ruhi004/w9-dh-app:latest'
                }
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }

        stage('Deploy') {
            steps {
                script {
                    bat 'minikube start'
                    bat 'kubectl apply -f my-kube1-deployment.yaml'
                    bat 'kubectl apply -f my-kube1-service.yaml'
                    echo 'Deployed successfully to Minikube!'
                }
            }
        }
    }
}
