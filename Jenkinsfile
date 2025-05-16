pipeline {
    agent any
    
    
tools {
        maven 'MAVEN3.9'   // Ensure this name matches Jenkins -> Global Tool Configuration
        jdk 'JDK17'        // Ensure this is set up in Jenkins tools too
    }
    
    stages {
        stage('Clone Repository') {
    steps {
        git branch: 'main', url: 'https://github.com/harishnshetty/Project-war2.git'
    }
}
stage('Build Maven Project') {
            steps {
                echo '🔧 Running mvn clean install...'
                sh 'mvn clean install'
            }
        }

        
        stage('Archive Build Artifacts') {
            steps {
                echo '📦 Archiving .jar or .war files...'
                archiveArtifacts artifacts: 'target/*.jar, target/*.war', fingerprint: true
            }
        }
        
         stage('Build Docker Image') {
            steps {
                echo '📦 Building Docker IMage...'
                sh 'docker build -t my-app:v1 .'
                sh 'docker run -d -p 9002:8080 --name my-app my-app:v1'
               
            }
        }

    }
}
