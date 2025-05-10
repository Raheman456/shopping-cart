pipeline{
    agent any

    stages{
        stage('scm'){
            steps{
                checkout scm
            }
        }
        stage('build'){
            steps{
                sh 'mvn clean install'
            }
        }
       stage('nexus'){
            steps{
                nexusArtifactUploader artifacts: [
                    [artifactId: 'shopping-cart', 
                    classifier: '', 
                    file: '/var/lib/jenkins/workspace/shopping-cart/target/shopping-cart-0.0.1-SNAPSHOT.war', 
                    type: 'war']
                    ], 
                    credentialsId: 'nexus', 
                    groupId: 'shopping-cart', 
                    nexusUrl: '34.224.22.246:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: 'shopping-cart', 
                    version: '0.0.1-SNAPSHOT'
            }
       }
       stage('tomcat'){
            steps{
                deploy adapters: [
                    tomcat9(
                        credentialsId: 'Tomcat', 
                        path: '', 
                        url: 'http://54.90.94.112:8090/')
                        ], 
                        contextPath: null, 
                        war: '**/*.war'
            }
       }
    }
}
