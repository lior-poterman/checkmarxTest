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
                    writeFile file: 'helloworld.py', text: "print('hello world')"
                }
            }
        }
        
        stage('Test') {
            steps {
                script {
                    // Display the content of helloworld.py using the 'type' command
                    bat 'type helloworld.py'
                }
            }
        }
        
        stage('Deploy') {
            steps {
                script {
                    // Copy the helloworld.py file to the repository directory
                    bat 'copy helloworld.py checkmarxTest\\'
                    
                    // The credentials you've configured in Jenkins will be used here
                    // Just specify the repository URL and Jenkins will handle authentication
                    def scmVars = checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/lior-poterman/checkmarxTest.git']]])
                    
                    // Commit and push the changes back to the repository
                    bat '''
                        cd checkmarxTest
                        git add helloworld.py
                        git commit -m "Update helloworld.py"
                        git push origin main  // Assuming main is the default branch
                    '''
                }
            }
        }
    }
}
