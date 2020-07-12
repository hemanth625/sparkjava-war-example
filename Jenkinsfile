pipeline {
    agent any
    stages{
        stage("codequality"){
            agent { docker 'maven:3-alpine' } 
                steps{
                    sh '''
            mvn sonar:sonar \
  -Dsonar.host.url=http://sonarqube.geeksstudy.com \
  -Dsonar.login=8c55cb317f9c2a24d7fd3e70557ef384c7fc2886
  '''
            }
        }
    }
}
