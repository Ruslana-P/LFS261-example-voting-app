pipeline {
    agent docker{
        image 'maven:3.9.8-sapmachine-21'
        args '-v $HOME/.m2:/root/.m2'
        }
    } 

    stages{
        stage("build"){
            steps{
                echo 'nuilding worker app'
                dir("worker") {
                    sh 'mvn compile'
                }
            }
        }
        stage("test"){
            steps{
                echo 'running unit tets on worker app'
                dir("worker") {
                    sh 'mvn clean test'
                }
            }
        }
        stage("package"){
            steps{
               echo 'packaging worker app into a jarfile'
                dir('worker'){ sh 'mvn package -DskipTests'
                archiveArtifacts artifacts:    '**/target/*.jar',
                    fingerprint: true
            }
        }
    } 

    post{
      always{
          echo 'This job is completed.'
      }
    }
}
