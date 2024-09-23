pipeline {
    agent any
    stages {
        stage('Source') {
            steps {
                // Run Docker container and execute Maven and Git commands inside it
                sh 'docker run --rm -v "$PWD":/usr/src/mymaven -w /usr/src/mymaven public.ecr.aws/docker/library/maven:3.9-sapmachine mvn --version'
                sh 'docker run --rm -v "$PWD":/usr/src/mymaven -w /usr/src/mymaven public.ecr.aws/docker/library/maven:3.9-sapmachine git --version'
                
                // Checkout source code from Git
                git branch: 'main',
                    url: 'https://github.com/bmukund21/docker-agent.git'
            }
        }
        stage('Clean') {
            steps {
                // Clean the project inside Docker container
                sh 'docker run --rm -v "$PWD":/usr/src/mymaven -w /usr/src/mymaven public.ecr.aws/docker/library/maven:3.9-sapmachine mvn clean'
            }
        }
        stage('Test') {
            steps {
                // Run tests inside Docker container
                sh 'docker run --rm -v "$PWD":/usr/src/mymaven -w /usr/src/mymaven public.ecr.aws/docker/library/maven:3.9-sapmachine mvn test'
            }
        }
        stage('Package') {
            steps {
                // Package the project inside Docker container, skipping tests
                sh 'docker run --rm -v "$PWD":/usr/src/mymaven -w /usr/src/mymaven public.ecr.aws/docker/library/maven:3.9-sapmachine mvn package -DskipTests'
            }
        }
    }
}
