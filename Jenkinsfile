pipeline {
    agent any
    stages {
        stage("code quality"){
            agent { docker 'maven:3-alpine' } 
            	steps {
               		sh '''
                    echo code quality step
                    '''
            }
        }
        stage('code build and publish') {
         	agent { docker 'maven:3-alpine' } 
            	steps {
               		sh 'mvn clean package'
                                           rtUpload (
    serverId: 'artifactory',
    spec: '''{
          "files": [
            {
              "pattern": "**/sparkjava-hello-world-1.0.war",
              "target": "project/"
            }
         ]
    }''',
    buildName: 'project',
    buildNumber: '1'
)
            }
        }
                    stage('deployment') {
                        agent {label 'slave01'}
            steps {
            sh'''
            id
            pwd
            cd /home/ubuntu/
            ls -lrt
            curl -uadmin:AP4t14ureDCjuExxrLJxT1BfdLf -O "http://13.58.132.104:8081/artifactory/project/sparkjava-hello-world-1.0.war"
            cp sparkjava-hello-world-1.0.war /opt/tomcat/webapps/
            '''
                }
            }
    }
}
