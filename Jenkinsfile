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
                // Copy WAR file to Tomcat webapps folder
                bat 'copy target\\MyWebApp-1.0-SNAPSHOT.war C:\\Tomcat\\apache-tomcat-9.0.110\\webapps\\MyWebApp.war'
                // Restart Tomcat
                bat ' C:\\Tomcat\\apache-tomcat-9.0.110\\bin\\shutdown.bat'
                bat ' C:\\Tomcat\\apache-tomcat-9.0.110\\bin \\startup.bat'
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
