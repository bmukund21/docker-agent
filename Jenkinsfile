pipeline {
    agent {
        docker { image 'public.ecr.aws/docker/library/maven:3.9-sapmachine' }
    }
    stages {
        stage('Source') {
            steps {
                // Display Maven and Git versions
                sh 'mvn --version'
                sh 'git --version'

                // Checkout source code from Git
                git branch: 'main',
                    url: 'https://github.com/bmukund21/docker-agent.git'
            }
        }
        stage('Clean') {
            steps {
                // Clean the project
                sh 'mvn clean'
            }
        }
        stage('Test') {
            steps {
                // Run tests
                sh 'mvn test'
            }
        }
        stage('Package') {
            steps {
                // Package the project and skip tests
                sh 'mvn package -DskipTests'
            }
        }
    }
}
