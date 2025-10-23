pipeline {
    //agent any
    agent {{image 'maven:3.6.3'}}

    stages {
        stage('Build') {
            steps {
                sh 'mvn --version'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
            }
        }
        stage('Integration Test') {
            steps {
                echo 'Integration Test...'
            }
        }
    }
    post {
        always {
            echo 'This will always run after the stages.'
        }
        success {
            echo 'This will run only if the pipeline succeeds.'
        }
        failure {
            echo 'This will run only if the pipeline fails.'
        }
    }
}