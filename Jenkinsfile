pipeline {
    agent docker { image 'node:20.16.0-alpine3.20' } 

    stages{
        stage("one"){
            steps{
                 sh 'node --version'
                 echo 'This step is completed AA.'
                sleep 10 
            }
        }


    } 

    post{
      always{
          echo 'This pipeline is completed.'
      }
    }
}
