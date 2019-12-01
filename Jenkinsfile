pipeline {
    agent any
    tools{
        maven 'local maven'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building......'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing......'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying......'
            }
        }
    }
}
