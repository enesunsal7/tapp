pipeline {
    agent any
    environment {
    DOTNET_CLI_HOME = "/tmp/DOTNET_CLI_HOME"
}
    stages {


        stage('Preparation') {
            steps {
                // Docker ajanına git
                script {
                    docker.image('mcr.microsoft.com/dotnet/sdk:8.0').inside('-v $PWD:/app') {
                        // Uygulama dizinine gidin
                        sh 'cd /app'
                        // Gerekli dosyaları kopyala ve bağımlılıkları yükle
                        sh 'dotnet restore'
                        // Uygulamayı derle
                        sh 'dotnet publish tapp.csproj -c Release -o out'
                        sh 'ls -la'
                        sh 'pwd'
                    }
                }
            }
        }
        
        stage('Deployment') {
            steps {
                // Docker ajanına git
                script {
                    docker.image('mcr.microsoft.com/dotnet/sdk:8.0').inside('-v $PWD:/app') {
                        // Çıktı dizinine git
                        sh 'ls -la'
                        sh 'pwd'
                        sh 'cd out'
                        sh 'pwd'
                        sh 'ls -la'
                        // Uygulamayı başlat
                        sh 'dotnet tapp.dll'
                    }
                }
            }
        }
    }
}
