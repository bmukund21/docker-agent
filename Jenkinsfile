pipeline {
    agent any
    stages {
        stage('Source') {
            agent {
                docker { image 'public.ecr.aws/docker/library/maven:3.9-sapmachine' }
            }
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
            agent {
                docker { image 'public.ecr.aws/docker/library/maven:3.9-sapmachine' }
            }
            steps {
                // Clean the project
                sh 'mvn clean'
            }
        }
        stage('Test') {
            agent {
                docker { image 'public.ecr.aws/docker/library/maven:3.9-sapmachine' }
            }
            steps {
                // Run tests
                sh 'mvn test'
            }
        }
        stage('Package') {
            agent {
                docker { image 'public.ecr.aws/docker/library/maven:3.9-sapmachine' }
            }
            steps {
                // Package the project and skip tests
                sh 'mvn package -DskipTests'
            }
        }
    }
}
