pipeline{
    agent any
    tools{
        maven 'local_maven'
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
                script{
                    readProp = readProperties file: 'build.properties'
                }
                echo "This is running on ${readProp['deploy.type']}"
                deploy adapters: [tomcat7(alternativeDeploymentContext: '', credentialsId: 'a35caabd-2856-4b60-ba00-9b8b684d2414', path: '', url: 'http://localhost:8081/')], contextPath: null, war: '**/*WAR'
            }
        }
    }
}