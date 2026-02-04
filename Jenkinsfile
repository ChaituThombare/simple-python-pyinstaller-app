pipeline {
    agent any

    stages {

        stage('Verify Python') {
            steps {
                bat 'where python'
                bat 'python --version'
            }
        }

        stage('Build') {
            steps {
                bat 'python -m py_compile sources\\add2vals.py sources\\calc.py'
            }
        }

        stage('Test') {
            steps {
                bat 'pytest --verbose sources\\test_calc.py'
            }
        }

        stage('Deliver') {
            steps {
                bat 'pyinstaller --onefile sources\\add2vals.py'
            }
            post {
                success {
                    archiveArtifacts 'dist\\*.exe'
                }
            }
        }
    }
}
