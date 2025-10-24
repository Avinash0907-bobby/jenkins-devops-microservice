pipeline {
    agent any
    //agent {docker{image 'maven:3.6.3'}}
    environment {
        dockerHome = tool 'Jenkins_Docker'
        mavenHome = tool 'Jenkins_Maven'
        PATH = "${env.mavenHome}/bin:${env.dockerHome}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                sh 'mvn --version'
            }
        }
        stage ('Compile') {
            steps {
                sh 'mvn clean compile'
            }
        }
        //stage('Test') {
          //  steps {
            //    sh 'mvn test'
            //}
        //}
        //stage('Integration Test') {
          //  steps {
            //    sh 'mvn failsafe:integration-test failsafe:verify'
            //}
        //}
        stage('Package') {
            steps {
                sh 'mvn package -DskipTests'
            }
        }
        stage('Build docker image') {
            steps {
               //"docker build -t mydockerbobby/currency-exchange:$env.BUILD_TAG"
               script {
                   dockerImage = docker.build("mydockerbobby/currency-exchange:${env.BUILD_TAG}")
               }
            }
        }
        stage('Push image to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                        dockerImage.push()
                        dockerImage.push('latest')
                    }
                }
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