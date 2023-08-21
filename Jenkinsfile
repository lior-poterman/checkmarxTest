pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout the repository
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    // Create the helloworld.py file with the specified content
                    echo "building the helloworld.py file.."
                    bat 'echo print("hello world") > helloworld.py'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Display the content of helloworld.py using the 'type' command
                    echo "Verifying the file content"
                    bat 'type helloworld.py'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo "Deploying code into GitHub"
                    // The credentials you've configured in Jenkins will be used here
                    // Just specify the repository URL and Jenkins will handle authentication
                    def scmVars = checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/lior-poterman/checkmarxTest.git']]])

                    // Commit and push the changes back to the repository
                    bat '''
                        git config user.name "lior-poterman"
                        git config user.email "liorpoterman@gmail.com"
                        git add helloworld.py
                        git commit -m "Update helloworld.py"
                        git push origin main
                    '''
                }
            }
        }
    }
}

