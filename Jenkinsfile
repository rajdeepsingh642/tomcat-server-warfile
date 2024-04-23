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
      
        stage('build') {
            steps {
             sh "mvn clean package"
            }
        }

        stage('tomcat') {
            steps {
            sshagent(['tomcat-server']) { 
                sh "scp -o StrictHostKeyChecking=no target/my-webapp.war tomcat@192.168.109.80:/home/tomcat/opt/tomcat/webapps"
                                    }
          
            }
        }    
   }


   
}