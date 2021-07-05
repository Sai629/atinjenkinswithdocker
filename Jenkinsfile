pipeline{
    agent{
        docker{
            image adoptopenjdk:latest
        }
    }
    triggers{
        pollSCM("* * * *")
    }
    stages{
        stage("test stage"){
            environment {CLASS_NAME='DEVOPS'}
            steps{
                sh 'java -version'
                sh 'echo $HOSTNAME'
                sh 'echo $CLASS_NAME'
            }
        }
    }
}