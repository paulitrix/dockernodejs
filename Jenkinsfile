pipeline {
    agent any

    environment {
          DEPLOY_URL = "https://example.com/"
          COMPOSE_FILE = "docker-compose.yml"
          DEPLOY_STACK_NAME = "hello"
          STACK_PREFIX = "web"
        }

         stages{
                stage('build') {
                         steps {
                                sh 'echo "Hi There!"'
                         }
                }

                stage('Verify Tools') {
                         steps {
                                parallel(
                                        docker: { sh "docker -v" },
                                        os: { sh "uname -a" }
                                )
                         }
                 }

                 stage('Create DB Volume') {
                          steps {
			      sh 'pwd'
                              sh 'docker volume create pgdata'
                              sh 'docker volume create app'
                          }
                  }

         }


        post {
                always {
			sh 'pwd'
			sh "docker-compose -f docker-compose.yml up -d --no-deps --build"
                        sh "docker service ls"
                        sh "docker container ls -q"
                        sh "echo Done!"

                 }
        }

}

