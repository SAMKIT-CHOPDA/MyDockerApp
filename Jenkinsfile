pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/SAMKIT-CHOPDA/MyWebApp2.git'
            }
        }
        stage('Build') {
            steps {
                echo 'Building with Maven...'
                bat 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
           steps {
        echo 'Deploying WAR to Tomcat...'
        // Copy WAR file
       bat 'copy target\\MyWebApp-1.0-SNAPSHOT.war C:\\Tomcat\\apache-tomcat-9.0.110\\webapps\\MyWebApp.war'

        // Stop Tomcat
        bat '%CATALINA_HOME%\\bin\\shutdown.bat'
        // Wait a few seconds to make sure Tomcat stops
        bat 'ping 127.0.0.1 -n 5 > nul'
        // Start Tomcat
        bat '%CATALINA_HOME%\\bin\\startup.bat'
    }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
