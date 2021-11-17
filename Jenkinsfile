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
            
            
            stage('Deploy') {
                steps {
                    script {
                        docker.withRegistry('', '243d2e83-d8f9-4992-923e-49aef413470d') {
                            dockerImage.push("v_$BUILD_NUMBER")
                            dockerImage.push("latest")
                        }
                    }
                }
            }
        }
    }