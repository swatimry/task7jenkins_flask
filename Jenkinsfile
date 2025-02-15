pipeline {
    agent any
    environment {
        PYTHON_PATH = 'C:\\Users\\ASUS\\AppData\\Local\\Programs\\Python\\Python313'
        PIP_PATH = 'C:\\Users\\ASUS\\AppData\\Local\\Programs\\Python\\Python313\\Scripts'
    }
    stages {
        stage('Install Dependencies') {
            steps {
                bat 'set PATH=%PYTHON_PATH%;%PIP_PATH%;%PATH% && python -m pip install -r requirements.txt'
            }
        }
       
        stage('Run Flask Application') {
            steps {
                bat 'set PATH=%PYTHON_PATH%;%PIP_PATH%;%PATH% && start /B python app.py'
            }
        }
        stage('Confirmation') {
            steps {
                bat 'curl -s http://127.0.0.1:5000/'
            }
        }
    }
}
