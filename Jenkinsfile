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
                if [ ! -f package.json ]; then
                    echo "Failed package.json is not"
                    exit 1
                fi

                if [ ! -f index.html ]; then
                    echo "Failed index.html is not"
                    exit 1
                fi

                if [ ! -f vite.config.js ];  then
                    echo "Failed vite.config.js is not"
                    exit 1
                fi

                echo "validate successfully"
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
                if [ -d dist ]; then
                    echo "Build Successfully"
                    ls -la dist
                else 
                    echo "Build Not crt"
                    exit /b 1
                fi
                '''
            }
        }


        stage("Archive"){
            steps{     
                archiveArtifacts artifacts: 'dist/**', fingerprint: true
                }
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