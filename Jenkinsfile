pipeline{
    agent { label 'AGENT-1' } //jenkins node name
    environment{
        PROJECT = 'expense'     //We can use these as global variables
        COMPONENT = 'backend' 
        DEPLOY_TO = "production"
        REGION = "us-east-1"
    }
    options{
        disableConcurrentBuilds()  //Builds will not applt at a time
        //timeout(time: 5, unit: 'SECONDS') //timeout after some metioned time
        timeout(time: 30, unit: 'MINUTES') // generally 30 min or based on project
    }
     parameters{
        string(name: 'version', description: 'Enter the application version')
    }
    stages{
        stage('Deploy'){
            steps{
                script{
                    withAWS(region: 'us-east-1', credentials: 'aws-creds') {
                        sh """
                            aws eks update-kubeconfig --region us-east-1 --name expense-dev
                            kubectl get nodes
                        """
                    }
                }
            }
        } 
    }
     
    post{
        always{
            echo 'I will always say Hello again!'
            deleteDir() //it will deletes the directory
        }
        failure{
            echo 'I will run when pipeline is failed'
        }
        success{
            echo 'I will run when pipeline is success'
        }
    }
}