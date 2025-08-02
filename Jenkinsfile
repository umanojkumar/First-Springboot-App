pipeline {
    agent any

    environment {
        DEPLOY_DIR = 'C:\\Users\\manojkumar\\Downloads\\helloworld'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/umanojkumar/First-Springboot-App.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Deploy') {
            steps {
                bat """
                if not exist "%DEPLOY_DIR%" mkdir "%DEPLOY_DIR%"
                copy /Y target\\helloworld-0.0.1-SNAPSHOT.jar "%DEPLOY_DIR%\\helloworld-0.0.1-SNAPSHOT.jar"
        
                REM Kill existing java processes (optional - be careful if other Java apps running)
                for /f "tokens=2 delims=," %%a in ('tasklist /FI "IMAGENAME eq java.exe" /FO CSV ^| findstr "java.exe"') do (
                    taskkill /PID %%a /F
                )
        
                REM Start in detached mode (detached cmd shell)
                start "" cmd /c "java -jar "%DEPLOY_DIR%\\helloworld-0.0.1-SNAPSHOT.jar" > "%DEPLOY_DIR%\\output.log" 2>&1"
                """
            }
        }
    }
}
