pipeline{
    agent {
    docker { image 'maven:3.9.6-eclipse-temurin-17' }
}
    
    stages{
        stage ('Build'){
            steps{
                sh 'mvn clean package'
            }
            post{
                success{
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deploy to tomcat server') {
            steps{
            
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', path: '', url: 'http://localhost:8888/')], contextPath: null, war: '**/*war'
            }
        }
    }
}
