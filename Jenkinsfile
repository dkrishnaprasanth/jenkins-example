pipeline {
    agent any


    stages {
        stage('SCM Checkout'){
          git 'https://github.com/dkrishnaprasanth/jenkins-example'
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
                sshagent(['tomcat_ssh'])
							{
  							sh ' scp -o StrictHostKeyChecking=no */target/*.war ec2-user@<172.31.39.44>:/var/lib/tomcat/webapps'
							}	
             }
   }
}
}
