pipeline {
    agent any


    stages {
        stage('SCM Checkout'){
          git 'https://github.com/pranikita/maven-project-1'
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
                 sshagent(['e7cfacc6-6e27-4d27-971b-0046352f9868']) {
                 sh 'scp -o StrictHostKeyChecking=no */target/*.war ec2-user@54.198.193.152:/var/lib/tomcat/webapps'
      } 
}
}
    }
}
