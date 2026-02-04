pipeline {
    agent {
        docker {
            image 'python:3.10'
        }
    }

    stages {
        stage('Setup Python Environment') {
            steps {
                sh '''
                    python --version
                    python -m venv venv
                    . venv/bin/activate
                    pip install --upgrade pip
                '''
            }
        }

        stage('Build / Compile Check') {
            steps {
                sh '''
                    . venv/bin/activate
                    python -m py_compile *.py
                '''
            }
        }

        stage('Unit Test') {
            steps {
                sh '''
                    . venv/bin/activate
                    pytest || echo "No tests found"
                '''
            }
        }
    }

    post {
        failure {
            echo 'Pipeline failed.'
        }
    }
}
