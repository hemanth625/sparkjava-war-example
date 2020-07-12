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

    }
}
