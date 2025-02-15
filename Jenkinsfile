pipeline {
    agent { label 'agent1' }

    environment {
        FLASK_PORT = "5000"
        VENV_PATH = "venv"
    }
    triggers {
        pollSCM('H/5 * * * *')  
    }


    stages {
        stage('Clone Repository') {
            steps {
                sh 'git --version'
                sh 'rm -rf task7jenkins_flask || true'
                sh 'git clone -b main https://github.com/swatimry/task7jenkins_flask.git'
                echo "Repository cloned successfully."
            }
        }

        stage('Set Up Virtual Environment') {
            steps {
                dir('task7jenkins_flask') {
                    sh 'python3 -m venv ${VENV_PATH}'
                    sh '. ${VENV_PATH}/bin/activate'  
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                dir('task7jenkins_flask') {
                    sh '. ${VENV_PATH}/bin/activate && pip install -r requirements.txt'
                }
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
                dir('task7jenkins_flask') {
                  sh """
                  . ${VENV_PATH}/bin/activate 
                  setsid python app.py --port=${FLASK_PORT} > flask.log 2>&1 &
                  """
                  sleep 5  
                  sh "tail -n 20 flask.log"  
                }
            }
       }

        
    }
}
