pipeline {
    agent any

    environment {
          DEPLOY_URL = "https://54.196.235.168/"
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
                              sh 'docker volume create pgdata'
                          }
                  }

         }


        post {
                always {
			sh "docker-compose  -f docker-compose.yml up -d --no-deps --build"
                        sh "docker service ls"
                        sh "docker container ls -q"
                        sh "echo Done!"

                 }
        }

}

