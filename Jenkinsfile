   pipeline {
      agent any
     
       stages {
            stage('Build') {
               steps {
                   script {
                        dockerImage = docker.build "jnv1123/spring_app"
                    }
               }
            }
            
            stage('Test') {
                steps {
                    echo 'Running unit tests ... '
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