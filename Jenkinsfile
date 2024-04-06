pipeline {
    environment {
        imagename = "suraj438/myproject"
        registryCredential = 'dockerhublogin'
        dockerImage = ''
    }
    agent any
    stages {
        stage('Cloning Git') {
            steps {
                git([url: 'https://github.com/SD1435/devops-project.git', branch: 'main'])
            }
        } // Added missing closing brace for 'Cloning Git' stage

        stage('Building image') {
            steps {
                script {
                    dockerImage = docker.build imagename
                }
            }
        }

        stage('Running image') {
            steps {
                script {
                    sh "docker run -d -p 8081:5000 ${imagename}:latest"
                }
            }
        }

        stage('Deploy Image') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push("$BUILD_NUMBER")
                        dockerImage.push('latest')
                    }
                }
            }
        }
    }
}
