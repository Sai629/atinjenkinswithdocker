// pipeline {
//     agent {
//         docker {
//             image 'adoptopenjdk/openjdk8-openj9:jre8u292-b10_openj9-0.26.0-ubuntu'
//             //maven image
//         }
//     }
//     triggers {
//         pollSCM("* * * *  *")
//     }
//     stages {
//         stage("test stage") {
//             environment {CLASS_NAME='DEVOPS'}
//             steps {
//                 sh 'java -version'
//                 sh 'echo $HOSTNAME'
//                 sh 'echo $CLASS_NAME'
//             }
//         }
//         stage("mvn"){
//             steps {
//                 sh 'mvn package -Dskipsteps'
//             }
//         }
//     }
// }



//parallel pipeline

pipeline{
    agent none
    triggers {
        pollSCM("* * * *  *")
    }
    stages {
        stage("prep"){
            agent{
            docker {
                image 'adoptopenjdk/openjdk8-openj9:jre8u292-b10_openj9-0.26.0-ubuntu'
            }
        }
            environment {CLASS_NAME='DEVOPS'}
            steps {
                sh 'java -version'
                sh 'echo $HOSTNAME'
                sh 'echo $CLASS_NAME'
            }

        stage("parallel"){
                failfast true
                parallel{
                    stage ("build on ubuntu"){
                        agent{
                            docker {
                                image 'adoptopenjdk:hotspot'
                             }
                        }
                    }
                    steps {
                         sh 'mvn install -DskipTests'
                    }
                    stage ("build java 11"){
                        agent{
                            docker {
                                image 'adoptopenjdk:8u292-b10-jre-hotspot'
                                //maven image
                             }
                        }
                        steps{
                            sh 'echo hello'
                        }
                    }
                }
            steps {
                sh 'mvn package -Dskipsteps'
            }
        }
    }
}
