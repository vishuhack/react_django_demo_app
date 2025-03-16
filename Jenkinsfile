pipeline{
    agent any
    
    stages{
        stage('Code'){
            steps{
                // echo "Cloning the repo from the GitHub"
                git url: 'https://github.com/vishuhack/react_django_demo_app.git/', branch: 'main'
            }
            
        }
        stage('Build'){
            steps{
                echo "Buliding the Project"
                sh 'docker build . -t vishveshdevops/django-todo-test:latest'
            }
            
        }
        stage('Push'){
            steps{
                echo "Pushing the Project"
                withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) 
                {
                    sh 'echo $dockerHubPassword | docker login -u $dockerHubUser --password-stdin'
                    sh 'docker push vishveshdevops/django-todo-test:latest'
                }
                // sh 'docker Build . -t vishveshdevops/django-todo-test:latest'
            }
            
        }
        stage('Test'){
            steps{
                echo "Test the new Build"
                // sh 'python3 -m pytest tests/test_foo.py --junitxml=pytest-report.xml'
            }
            
        }
        stage('Deploy'){
            steps{
                echo "Deploy the website nn to server"
                sh 'docker-compose down && docker-compose up -d --no-deps --build'
            }
            
        }
    }
}