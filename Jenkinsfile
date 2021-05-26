pipeline {
    agent any
    
    tools {
        nodejs 'myNodeJS'
    }
    
    stages {
        stage('Build') {
            steps {
                echo 'BUILDING' 
                sh "npm install"
            }
        }
        stage('Unit Test') {
            steps {
                echo 'UNIT TESTING'
                sh "npm test"
            }
        }
        stage('Create Docker Image') {
            steps {
                echo 'CREATE DOCKER IMAGE'
                withCredentials([usernamePassword(credentialsId: 'DockerRepo', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')]) {
                    sh '''
                        wget https://download.docker.com/linux/ubuntu/dists/bionic/pool/stable/amd64/docker-ce-cli_18.09.9~3-0~ubuntu-bionic_amd64.deb
                        dpkg -i ./docker-ce-cli_18.09.9~3-0~ubuntu-bionic_amd64.deb
                        apt-get update
                        apt-get install -y awscli
                        docker build -t workshopuser8:latest .
                        docker tag workshopuser8:latest workshopuser8:${BUILD_NUMBER}
                        docker tag workshopuser8:latest 686567993080.dkr.ecr.us-east-1.amazonaws.com/devopsbootcampuser8:latest
                        $(aws ecr get-login --region us-east-1 | sed 's/-e none//g')
                        docker push 686567993080.dkr.ecr.us-east-1.amazonaws.com/devopsbootcampuser8:latest
                    '''
                }
            }
        }
    }
}