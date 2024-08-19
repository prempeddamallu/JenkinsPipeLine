pipeline{
    agent any
    environment{
        Docker_Image="calculator-app:latest"
    }
    triggers {
        pollSCM('*/1 * * * *')
    }
    stages{
        stage("SCM"){
            steps{
                git branch: 'main', url: 'https://github.com/prempeddamallu/JenkinsPipeLine.git'

            }
        }
        stage("Test"){
            steps{
                bat 'C:\\Users\\PremKumarReddyPeddam\\AppData\\Local\\Programs\\Python\\Python312\\python.exe -m unittest discover'
            }
        }
        stage("Build"){
            steps{
                bat "docker build . -t ${Docker_Image}"
            }
        }
        stage("Deploy"){
            steps{
            bat "docker ps -a | findstr PythonContainer1 && docker stop PythonContainer1 && docker  rm PythonContainer1 || exit /b 0"
            bat "docker run -d -p 5000:5000 --name PythonContainer1 ${Docker_Image}"
                                                   
            }
        }
    }
    post{
        success{
            echo "Successfully Deployed"
        }
        failure{
            echo "Failed to Deploy"
        }
    }
}
