pipeline {
    agent any

    stages {
        stage('Build with Maven') {
            steps {
                script {
                    // Clean and build with Maven
                    def mavenHome = tool 'maven3'
                    def mavenCMD = "${mavenHome}/bin/mvn"

                    sh "${mavenCMD} clean install"
                }
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                script {
                    // Tomcat configuration
                    def tomcatUrl = 'http://localhost:9090/'
                    def tomcatManagerUser = 'root'
                    def tomcatManagerPassword = 'root'
                    def warFileName = 'web-application'


                    // Deploy to Tomcat with context path
                     withCredentials([usernamePassword(credentialsId: 'adcdb82f-8ab0-4c05-932b-bdfe05566092', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                       sh "curl -v --user ${USERNAME}:${PASSWORD} --upload-file target/${warFileName} ${tomcatUrl}/manager/text/deploy?path=web-application&update=true"
                      }
                }
            }
        }
    }
}
