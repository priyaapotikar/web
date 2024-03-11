pipeline{
    agent{
        label "Linux_Slave"
    }
    stages{
        stage("Down Container with docker-compose"){
            steps{
                echo "========executing container is exiting========"
                sshPublisher(publishers: [sshPublisherDesc(configName: 'Deep_Sites_Docker', transfers: [sshTransfer( execCommand: '''cd /home/ubuntu/hr-sndk-corp
                sudo docker-compose down -v --rmi all''', execTimeout: 120000)], verbose: true)])
            }
            post{
                always{
                    echo "========always========"
                }
                success{
                    echo "========Container exited successfully========"
                }
                failure{
                    echo "========Container exited failed========"
                }
            }
        }
        stage("SCM"){
            steps{
                echo "====++++executing Pulling the code form GitHub++++===="
                sshPublisher(publishers: [sshPublisherDesc(configName: 'Deep_Sites_Docker', transfers: [sshTransfer( execCommand: '''cd /home/ubuntu/hr-sndk-corp
                git stash
                git pull origin master''', execTimeout: 120000)], verbose: true)])
            }
            post{
                always{
                    echo "====++++always++++===="
                }
                success{
                    echo "====++++SCM executed successfully++++===="
                }
                failure{
                    echo "====++++SCM execution failed++++===="
                }

            }
        }
        stage("Run container with docker-compose"){
            steps{
                echo "====++++executing UP container with docker-compose++++===="
                sshPublisher(publishers: [sshPublisherDesc(configName: 'Deep_Sites_Docker', transfers: [sshTransfer( execCommand: '''cd /home/ubuntu/hr-sndk-corp
                sudo docker-compose up -d''', execTimeout: 120000)], verbose: true)])
            }
            post{
                always{
                    echo "====++++always++++===="
                }
                success{
                    echo "====++++container running successfully++++===="
                }
                failure{
                    echo "====++++container running failed++++===="
                }

            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
