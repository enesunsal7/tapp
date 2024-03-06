pipeline {
    agent {
        docker {
            image 'mcr.microsoft.com/dotnet/sdk:8.0'
        }
    }

    stages {
        stage('Preparation') {
            steps {
                // Preparation steps such as restoring dependencies
                sh 'dotnet restore'
            }
        }
        
        stage('Build') {
            steps {
                // Building the .NET application
                sh 'dotnet build'
            }
        }
        
        stage('Publish') {
            steps {
                // Publishing the .NET application
                sh 'dotnet publish tapp.csproj -c Release -o out'
            }
        }
        
        stage('Deploy') {
            steps {
                // Setting up environment variable
                sh 'export ASPNETCORE_URLS="http://*:1453"'
                
                // Running the .NET application
                sh 'dotnet out/tapp.dll'
            }
        }
    }
}
