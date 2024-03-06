pipeline {
    agent any
    
    stages {

        environment {
   HOME = '/tmp'
} 
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
                        sh 'cd /app/out'
                        // Uygulamayı başlat
                        sh 'dotnet tapp.dll'
                    }
                }
            }
        }
    }
}
