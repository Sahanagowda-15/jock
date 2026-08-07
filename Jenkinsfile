pipeline
{
    agent any
    stages{
        stage('continousdownload')
        {
            steps
            {
                git 'https://github.com/Sahanagowda-15/maven.git'
            }
        }
        stage('continousbuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('continousdeployment')
        {
            steps{
                   deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'e2aa16de-e9c7-4cf1-a21d-8b86d8c64ef7', path: '', url: 'http://172.31.11.85:8080')], contextPath: 'test', war: '**/*.war'
            }
        }
        stage('continousTesting')
        {
            steps{
                git 'https://github.com/Sahanagowda-15/functional.git'
                sh 'java -jar /home/ubuntu/.jenkins/workspace/gon/testing.jar'
            }
        }
        stage('continousDelivery')
        {
            steps{
                input message:'waiting for approval from the DM',submitter:'sahana'
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: '17a0df7f-57c8-40f9-bc38-64a8779f3459', path: '', url: 'http://172.31.10.254:8080')], contextPath: 'prod', war: '**/*.war'
            }
        }
    }
}
