def gv

pipeline {
    agent any
   
    stages {
        stage("build") {
            steps {
                echo 'building the application ...'
                echo 'build done'
            }
        }
    
        stage("test") {
            steps {
                echo 'testing the application ...'
                echo 'test done'
            }
        }
        stage("deploy") {
            steps {
               echo 'deploying the application ...'
                echo 'deploy done'
            }
        }
    }   
}
