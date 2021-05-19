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
    }
}