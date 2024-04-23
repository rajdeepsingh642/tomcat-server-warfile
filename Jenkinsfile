pipeline {
    agent any
    tools{
        jdk "jdk17"
        maven "maven3"
    }

   stages {
        stage('git checkout') {
            steps {
               git branch: 'main', url: 'https://github.com/rajdeepsingh642/tomcat-server-warfile.git'
            }
        }
        stage('compile') {
            steps {
             sh "mvn compile"
             }
        }    
       
        stage('build') {
            steps {
             sh "mvn package -DskipTests"
            }
        }

        stage('tomcat') {
            steps {
            sshagent(['tomcat-server']) { 
                sh "scp -o StrictHostKeyChecking=no target/demo-maven.jar tomcat@192.168.109.80:/home/tomcat/opt/tomcat/webapps"
                                    }
          
            }
        }    
   }


   
}