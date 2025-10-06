pipeline {
    agent any

    environment {
        IMAGE_NAME = "mydockerapp"
        CONTAINER_NAME = "myapp_container"
    }

   

        stage('Build Application') {
            steps {
                echo 'Installing dependencies...'
                bat 'pip install -r requirements.txt'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                bat 'docker build -t %IMAGE_NAME% .'
            }
        }

        stage('Run Docker Container') {
            steps {
                echo 'Running container...'
                bat '''
                docker ps -q --filter "name=%CONTAINER_NAME%" > tmp.txt
                for /f %%i in (tmp.txt) do docker stop %%i && docker rm %%i
                docker run -d --name %CONTAINER_NAME% -p 5000:5000 %IMAGE_NAME%
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Application built, dockerized, and running!'
        }
        failure {
            echo '❌ Build failed. Check Jenkins logs.'
        }
    }
}
