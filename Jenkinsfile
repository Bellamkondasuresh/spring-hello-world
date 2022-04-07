pipeline { 
    agent{ label "MASTER" }
    triggers{ pollSCM('* * * * *') }
    stages{
        stage ('Code Download From GIT'){
            steps{
                git 'https://github.com/Bellamkondasuresh/spring-hello-world.git'
            }
        }
         
        stage('Deploy_Server_setup'){
            steps{
                sh "ansible -m ping -i $WORKSPACE/spring-hello-world/inventory all"
                sh "ansible-playbook -i $WORKSPACE/spring-hello-world/inventory $WORKSPACE/myplaybook.yml --syntax-check"
                sh "ansible-playbook -i $WORKSPACE/spring-hello-world/inventory $WORKSPACE/myplaybook.yml"
            }            
        }
        stage('Deploy'){
            agent{ label "deploy_server"}
            steps{
                sh "cd /home/jenkins"
                sh "sudo docker image build -t ceq_spring:1.0 ."
                sh "sudo docker container run -d -p 8081:8081 ceq_spring:1.0 "
                           
            }
        } 
    }
}
