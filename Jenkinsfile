pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                echo "Build Docker Image"
                bat "docker build -t kubedemoapp:v1 ."
            }
        }
        stage('Docker Login') {
            steps {
                bat 'docker login -u pushkara16 -p Smiley16*'
            }
        }
        stage('Push Docker Image to Docker Hub') {
            steps {
                echo "push Docker Image to Docker Hub"
                bat "docker tag kubedemoapp:v1 pushkara16/sample:kubeimage1"

                bat "docker push pushkara16/sample:kubeimage1"
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                // apply deployment & service
                bat 'kubectl apply -f deployment.yaml --validate=false'
                bat 'kubectl apply -f service.yaml'
            }
        }
    }
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
}
