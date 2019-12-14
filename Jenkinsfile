pipeline {
    agent any


    stages {
        stage('SCM Checkout'){
          git 'https://github.com/AvijitChd/jenkins-example.git'
        }
  }
    {
        stage ('Compile Stage') {

            steps {
                withMaven(maven : 'LocalMaven') {
                    sh 'mvn clean compile'
                }
            }
        }

        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'LocalMaven') {
                    sh 'mvn test'
                }
            }
        }


        stage ('install Stage') {
            steps {
                withMaven(maven : 'LocalMaven') {
                    sh 'mvn install'
                }
            }
        }

        
         stage ('deploy to tomcat') {
             steps {
                 sshagent(['tomcats']) {
                 sh 'scp -o StrictHostKeyChecking=no target/*.jar ec2-user@52.15.167.231:/var/lib/tomcat/webapps/'
      }
             }
   }
}
}
