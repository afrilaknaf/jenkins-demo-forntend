pipeline{
    agent any

    stages{
        stage("Checkout"){
            steps{
                git branch : "master",
                url : "https://github.com/afrilaknaf/jenkins-demo-forntend.git"
            }
        }

        stage("Validate"){
            steps{
                sh '''
                echo Validate the forntend 
                if not exist package.json (
                    echo Failed package.json is not
                    exit /b 1
                )

                if not exist index.html (
                    echo Failed index.html is not
                    exit /b 1
                )

                if not exist vite.config.js (
                    echo Failed vite.config.js is not
                    exit /b 1
                )
                '''
            }
        }


        stage("Install"){
            steps{
                sh '''  
                echo Install Node.js Depencies 
                npm ci
                '''
            }
        }

        stage("Build React App"){
            steps{
                sh '''
                echo Build the react project
                npm run build
                '''
            }
        }


        stage("CheckBuild"){
            steps{
                sh '''
                echo Check the dist folder
                if exist dist (
                    echo Build Successfully
                    dir dist
                ) else (
                    echo Build Not crt
                    exit /b 1
                )
                '''
            }
        }


        stage("Archive"){
            steps{     
                archiveArtifacts artifacts: 'dist/**', fingerprint: true
                }
        }
    }


    post {

        success {
            echo "Frontend Build Completed Successfully"
        }

        failure {
            echo "Frontend Build Failed"
        }

        always {
            echo "Pipeline Finished"
        }
    }
}