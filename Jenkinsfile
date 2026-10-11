pipeline {
    agent none

    stages {
        stage('build') {
            when {
                changeset '**/worker/**'
            }
            agent {
                docker {
                    image 'maven:3.9.8-sapmachine-21'
                    args '-v $HOME/.m2:/root/.m2'
                }
            }
            steps {
                dir('worker') {
                    sh 'mvn compile'
                }
            }
        }

        stage('test') {
            when {
                changeset '**/worker/**'
            }
            agent {
                docker {
                    image 'maven:3.9.8-sapmachine-21'
                    args '-v $HOME/.m2:/root/.m2'
                }
            }
            steps {
                dir('worker') {
                    sh 'mvn test'
                }
            }
        }

        stage('package') {
            when {
                branch 'master'
                changeset '**/worker/**'
            }
            agent {
                docker {
                    image 'maven:3.9.8-sapmachine-21'
                    args '-v $HOME/.m2:/root/.m2'
                }
            }
            steps {
                dir('worker') {
                    sh 'mvn package'
                }
            }
        }

        stage('docker-package') {
            when {
                branch 'master'
                changeset '**/worker/**'
            }
            agent any
            steps {
                script {
                    docker.withRegistry('https://registry-1.docker.io', 'dockerlogin') {
                        def customImage = docker.build("student1mouse/worker:v${env.BUILD_ID}", "./worker")
                        customImage.push()
                        customImage.push('latest')
                    }
                }
            }
        }
    }
}
