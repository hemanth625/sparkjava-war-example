pipeline {
    agent any
    stages {
        stage("code quality"){
            agent { docker 'maven:3-alpine' } 
            	steps {
               		sh '''
                    mvn sonar:sonar \
  -Dsonar.projectKey=myproject \
  -Dsonar.host.url=http://18.222.168.48:9000 \
  -Dsonar.login=449553e2ad6827094f24d21c56b7be7a72cd47d9   
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
            agent any
            steps {
            sh'''
            curl -uadmin:AP46TAKYYmbBUgTfoobH6y8gevM -O "http://18.189.189.172:8081/artifactory/project/sparkjava-hello-world-1.0.war"
            ls -lrt
            mydir=`pwd`
            sshpass -p "1234" scp -r root@3.15.176.104:/opt/tomcat/webapps/ $mydir/sparkjava-hello-world-1.0.war
            cp sparkjava-hello-world-1.0.war /opt/tomcat/webapps/
            '''
                }
            }

    }
}
