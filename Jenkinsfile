   pipeline {
      agent any
     
       stages {
            stage('Checkout') {
                steps {
                    checkout scm
                }
            }
            
            stage('Test') {
                steps {
                    echo 'Running unit tests ... '
                }
            }
            
            stage('Build') {
               steps {
                   script {
                        dockerImage = docker.build "jnv1123/spring_app"
                    }
               }
            }
            
            stage('Push') {
                steps {
                    script {
                        docker.withRegistry('','243d2e83-d8f9-4992-923e-49aef413470d') {
                            dockerImage.push("$BUILD_ID")
                            dockerImage.push("latest")
                            }
                        }
                    }
            }
            
            
            stage('Deploy') {
                steps {
                    script {
                        withAWS(region: 'us-east-1', credentials: '43112608-9288-411a-8cd0-13a970e351d5') {
                            sh "aws ecs register-task-definition \
                               --family first-run-task-definition \
                               --cli-input-json file://taskdef.json"
                            
                            sh "aws ecs update-service --service custom-service --cluster test --force-new-deployment"
                        }
                    }
                }
            }
        }
    }