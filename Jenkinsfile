pipeline{
    agent any

    stages{
        stage('Sonar Quality Check'){
//             agent {
//                docker {
//                    image 'openjdk:11'
//                }
//            }

            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'sonar-token') {
                         sh 'chmod +x gradlew'
                         sh './gradlew sonarqube'
 //                        sh './gradlew sonarqube --debug output'
                      }

                      timeout(time: 1, unit: 'HOURS') {
                      def qg = waitForQualityGate()
                      if (qg.status != 'OK') {
                           error "Pipeline aborted due to quality gate failure: ${qg.status}"
                      }
                    }
                }
            
            }
        }
    }
}