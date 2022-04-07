pipeline { 
    agent{ label "MASTER" }
    triggers{ pollSCM('* * * * *') }
    stages{
        stage ('Code Download From GIT'){
            steps{
                sh "git clone https://github.com/Bellamkondasuresh/spring-hello-world.git"
            }
        }
         
        
     
