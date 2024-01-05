def gv

pipeline {
    agent any
   
    stages {
        stage("build") {
            steps {
                echo 'building the application ...'
                echo 'build done'
                switch(CLIENT){
 case "Client1":
return ["Tests1", "Tests11", "Tests111"]
 break
case "Client2":
    return ["Tests2", "Tests22", "Tests222", "Tests2222"]
break
 case "Client3":
    return ["Tests3", "Tests33", "Tests333"]
 break
} 
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
