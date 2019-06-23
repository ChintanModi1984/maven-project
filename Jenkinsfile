pipeline {
    agent any
    tools {
        maven 'maven3'
        jdk 'java8'
    }
    
    stages {
        stage ('init') {
            steps {
                echo "This is Initializing Stage"
            }
        }
        stage ('Build') {
            steps {
                echo "This is build stage"
                
            }
            post {
                success {
                    echo "Archive Arteffect"
                    archiveArtifacts '**/*.war'
                    echo "publish junit meter"
                    junit '**/surefire-reports/*.xml'
                    echo "check analysis result"
                    checkstyle canComputeNew: false, defaultEncoding: '', healthy: '', pattern: 'clean package checkstyle:checkstyle', unHealthy: ''

                }
            }
        }
        stage ('Deploy') {
            steps {
          
                     timeout(time: 30, unit: 'SECONDS') {
   
                            input 'Do you want to proceed ?'
                                                       }          
                build  'JenkinsFirstProject'
            }
        }
    }
}

