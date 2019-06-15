pipeline {
    agent any


    stages {
        stage('SCM Checkout'){
          git 'https://github.com/prakashk0301/maven-project.git'
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

        stage ('build && SonarQube analysis') {
            steps {
		withSonarQubeEnv(credentialsId:'sonar') {
                    withMaven(maven : 'LocalMaven') {
                        sh 'mvn clean package sonar:sonar'
                    }
		}	
            }
        }
}
}
