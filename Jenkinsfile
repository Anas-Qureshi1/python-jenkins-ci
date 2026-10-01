pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                checkout scm
            }
        }

        stage('Python Version') {
            steps {
                echo 'Checking Python version...'

                bat '''
                python --version
                python -m pip --version
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing Python dependencies...'

                bat '''
                python -m pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running pytest...'

                bat '''
                python -m pytest
                '''
            }
        }

        stage('Generate Test Report') {
            steps {
                echo 'Generating HTML test report...'

                bat '''
                if not exist reports mkdir reports
                python -m pytest --html=reports/test-report.html --self-contained-html
                '''
            }
        }

        stage('Build') {
            steps {
                echo 'Python CI build completed successfully!'
            }
        }
    }

    post {

        success {
            echo '===================================='
            echo 'PYTHON CI PIPELINE SUCCESSFUL'
            echo '===================================='
        }

        failure {
            echo '===================================='
            echo 'PYTHON CI PIPELINE FAILED'
            echo '===================================='
        }

        always {
            echo 'Pipeline execution completed.'
        }
    }
}