pipeline {
    agent any

    stages {
        stage('git checkout') {
            steps {
                git branch: 'main', credentialsId: 'bhanu', url: 'https://github.com/baludravid/newlms'
            }
        }
        stage ('maven build') {
            steps{
                sh 'mvn clean package '
            }
        }
         stage('Dev Deploy') {
            steps {
                sshagent(['newbhanu']) {
           
            // copy war file tomcat to dev server 
            sh "scp -o StrictHostKeyChecking=no target/newlms.war ec2-user@172.31.47.209:/opt/tomcat9/webapps"
       
        // stop the tomcat 
                    sh "ssh ec2-user@172.31.47.209 /opt/tomcat9/bin/shutdown.sh"
        
                    // start the tomcat
                     sh "ssh ec2-user@172.31.47.209 /opt/tomcat9/bin/startup.sh"
                         }
                }
            }
        }
    }

                
