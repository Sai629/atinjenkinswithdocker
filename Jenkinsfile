pipeline {
    agent {
        docker {
            image 'adoptopenjdk/openjdk8-openj9:jre8u292-b10_openj9-0.26.0-ubuntu'
        }
    }
    triggers {
        pollSCM("* * * *")
    }
    stages {
        stage("test stage") {
            environment {CLASS_NAME='DEVOPS'}
            steps {
                sh 'java -version'
                sh 'echo $HOSTNAME'
                sh 'echo $CLASS_NAME'
            }
        }
    }
}