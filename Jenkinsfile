pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Setup Environment') {
            steps {
                sh 'python3 -m venv venv'
                sh '. venv/bin/activate && pip install -r requirements.txt'
            }
        }

        stage('Run Model Prediction') {
            steps {
                sh '. venv/bin/activate && python predict.py --duration 120 --jobs 6 --team_size 8'
            }
        }
    }
}
