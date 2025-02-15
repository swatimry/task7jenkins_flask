pipeline {
    agent any
    stages {
       
        stage('Install Dependencies') {
            steps {
                bat 'pip install -r requirements.txt'
            }
        }
       
        stage('Run Flask Application') {
            steps {
                bat 'start /B python app.py'
            }
        }
        stage('Confirmation') {
            steps {
                bat 'curl -s http://127.0.0.1:5000/'
            }
        }
    }
}
