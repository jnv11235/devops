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
                        docker.withRegistry('', 'credentials-id') {
                            dockerImage.push("v_$BUILD_NUMBER")
                            dockerImage.push("latest")
                        }
                    }
                }
            }
        }
    }