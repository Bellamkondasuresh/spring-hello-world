pipeline { 
    agent{ label "MASTER"}
    stages{
        stage ('Code Download From SCM'){
            steps{
                git 'https://github.com/Bellamkondasuresh/spring-hello-world.git'
                stash name: 'Dockerfile', includes: 'Dockerfile'
            }
        }
        stage('GOF Docker Run'){
            agent{ label "docker-slave" }
            steps{
                dir('/home/jenkins'){
                      unstash name: 'Dockerfile'                                                                                           
                }   
                sh '''
                   docker image build -t hairavi10/gameoflife:05.20 /home/jenkins
                   docker run -d -p 8081:8080 suresh9177/gameoflife:05.20
                   '''
            }
        }
        
    }
