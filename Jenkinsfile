pipeline {
    
    agent {
        node {
            label 'python'
        }
    }

    environment {
        HELLO_MESSAGE = 'Barevki'
    }


    stages {

        stage("Hello step") { 
            steps {
                echo "Hello World from Jenkins"
                echo "building version ${HELLO_MESSAGE}"
                sh 'python3 --version'
            }
        }


        stage("Pytest") { 
            steps {
                echo "This is Pytest stage"
                sh "pytest -rp calculator_pytest.py"

            }
        }
        
        stage("Unittest") { 
            steps {
                echo "This is Unittest stage"
                sh "python3 -m unittest -v calculator_unittest.py"
            }
        }
        
        stage("Deploy") { 
            when {
              expression { currentBuild.result == null || currentBuild.result == 'SUCCESS' }
            }
            steps {
                echo "This is Deployment stage"
                sh "python3 calculator.py"
            }
        }
    post {
        always {
            echo "Number of this build ${BUILD_NUMBER}"
        }
    }
    }
}
