pipeline {
    agent any


    stages {
        stage('SCM Checkout'){
          git 'https://github.com/payalBonde/jenkins-example'
        }
  }
    {
        stage ('Compile Stage') {

            steps {
                withMaven(maven : 'localMaven') {
                    sh 'mvn clean compile'
                }
            }
        }

        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'localMaven') {
                    sh 'mvn test'
                }
            }
        }


        stage ('install Stage') {
            steps {
                withMaven(maven : 'localMaven') {
                    sh 'mvn install'
                }
            }
        }

         stage ('deploy to tomcat') {
             steps {
                 sshagent(['tomcat1']) {
                 sh 'scp -o StrictHostKeyChecking=no target/*.jar ec2-user@18.224.149.75:/var/lib/tomcat/webapps/'
      }
             }
   }
}
}
