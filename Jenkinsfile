pipeline {
    agent any

    environment {
        PROJECT_DIR = '/home/a/tkti'
        VENV_DIR = '/home/a/tkti/venv'
    }

    stages {
        stage('Setup Environment') {
            steps {
                dir("${env.PROJECT_DIR}") {
                    sh '''
                    echo "🔧 Setting up virtual environment..."
                    python3 -m venv venv
                    source venv/bin/activate
                    pip install -r requirements.txt
                    '''
                }
            }
        }

        stage('Run Tests') {
            steps {
                dir("${env.PROJECT_DIR}") {
                    sh '''
                    echo "🧪 Running tests..."
                    source venv/bin/activate
                    pytest --maxfail=1 --disable-warnings -q
                    '''
                }
            }
        }

        stage('Build Artifact') {
            steps {
                dir("${env.PROJECT_DIR}") {
                    sh '''
                    echo "📦 Building artifact..."
                    mkdir -p build
                    zip -r build/app.zip src
                    echo "✅ Build artifact created at build/app.zip"
                    '''
                }
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline sukses dijalankan di /home/a/tkti!'
        }
        failure {
            echo '❌ Pipeline gagal!'
        }
    }
}
