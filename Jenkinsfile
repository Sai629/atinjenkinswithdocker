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
    agent none;
    triggers {
        pollSCM("* * * *  *")
    }
    stages {
        agent{
            docker {
                image 'adoptopenjdk/openjdk8-openj9:jre8u292-b10_openj9-0.26.0-ubuntu'
            //maven image
            }
        }
        stage("test stage") {
            environment {CLASS_NAME='DEVOPS'}
            steps {
                sh 'java -version'
                sh 'echo $HOSTNAME'
                sh 'echo $CLASS_NAME'
            }
        }
        stage("parallel"){
                failfast true
                parallel{
                    stage ("build on ubuntu"){
                        agent{
                            docker {
                                image 'adoptopenjdk/openjdk8-openj9:jre8u292-b10_openj9-0.26.0-ubuntu'
                                //maven image
                             }
                        }
                    }
                    steps {
                         sh 'mvn install -DskipTests'
                    }
                    stage ("build java 11"){
                        agent{
                            docker {
                                image 'adoptopenjdk/openjdk8-openj9:jre8u292-b10_openj9-0.26.0-ubuntu'
                                //maven image
                             }
                        }
                        steps{
                            sh 'mvn install'
                        }
                    }
                }
            steps {
                sh 'mvn package -Dskipsteps'
            }
        }
    }
}
    post {
        always {
            echo "hello workd"
        }
        unsucessful {
            sh 'failed'
        }
    } 