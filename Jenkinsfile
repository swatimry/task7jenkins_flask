pipeline {
    agent { label 'agent1' }

    environment {
        FLASK_PORT = "5000"
        VENV_PATH = "venv"
    }
    stages {
        stage('Checkout Code') {
            steps {
                checkout scm  
            }
        }

        stage('Set Up Virtual Environment') {
            steps {
                sh 'python3 -m venv ${VENV_PATH}'
                sh '. ${VENV_PATH}/bin/activate'  
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '. ${VENV_PATH}/bin/activate && pip install -r requirements.txt'
            }
        }

        stage('Stop Existing Flask App') {
            steps {
                script {
                    sh "pkill -f 'python3 app.py' || true"
                }
            }
        }

        stage('Run Flask App') {
            steps {
                sh ". ${VENV_PATH}/bin/activate && nohup python app.py --port=${FLASK_PORT} > flask.log 2>&1 &"
                sleep 5  
                sh "tail -f flask.log"  
            }
        }
    }
}
