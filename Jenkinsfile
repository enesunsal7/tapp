pipeline {
    agent any

    stages {
         stage('Preparation') {
            steps {

                sh  'FROM mcr.microsoft.com/dotnet/sdk:8.0'
                // Installing required packages
                sh 'dotnet restore'
                
                // Code inspection and quality control
                sh 'dotnet analyze'
                
                // Updating dependencies
                sh 'dotnet nuget update --self'
                
                // Running preparation tests
                sh 'dotnet test'
            }
        }
        stage('Build') {
            steps {
                // Building the .NET application
                sh 'dotnet build'
            }
        }
        
        stage('Package') {
            steps {
                // Packaging .NET application into a Docker container
                sh 'docker build -t tappjenkins:v1 .'
            }
        }
        
        stage('Deploy to Private Registry') {
            steps {
                // Log in to the private Docker registry
                sh 'docker login -u master -p Password1 http://registry.enes.local:5000'
                
                // Tagging the Docker image
                sh 'docker tag tappjenkins:v1 http://registry.enes.local:5000/tappjenkins:v1'
                
                // Pushing the Docker image to the private registry
                sh 'docker push http://registry.enes.local:5000/tappjenkins:v1'
            }
        }
        
        // Other stages can be added here
    }
}
