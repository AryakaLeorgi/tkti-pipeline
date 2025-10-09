pipeline {
    agent any

    environment {
        PROJECT_DIR = 'tkti'
        VENV_DIR = 'venv'
    }

    stages {
        stage('Setup Environment') {
            steps {
                sh '''
                echo "🔧 Setting up virtual environment..."
                python3 -m venv venv
                source venv/bin/activate
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                echo "🧪 Running tests..."
                source venv/bin/activate
                pytest --maxfail=1 --disable-warnings -q
                '''
            }
        }

        stage('Build Artifact') {
            steps {
                sh '''
                echo "📦 Building artifact..."
                mkdir -p build
                zip -r build/app.zip src
                echo "✅ Build artifact created at build/app.zip"
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline sukses dijalankan!'
        }
        failure {
            echo '❌ Pipeline gagal!'
        }
    }
}
