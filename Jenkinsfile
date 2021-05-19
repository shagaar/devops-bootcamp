pipeline {
    agent any
    
    tools {
        nodejs 'myNodeJS'
    }
    
    stages {
        stage('Hello') {
            steps {
                echo 'Hello World' 
                sh "npm install"
            }
        }
    }
}