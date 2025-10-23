pipeline {
    agent any
    //agent {docker{image 'maven:3.6.3'}}
    environment {
        dockerHome = tool 'Jenkins_Docker'
        mavenHome = tool 'Jenkins_Maven'
        PATH = "${env.mavenHome}/bin:${env.dockerHome}/bin:${env.PATH}"
    }

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