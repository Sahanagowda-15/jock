pipeline
{
    agent any
    stages{
        stage('continousdownload')
        {
            steps
            {
                git 'https://github.com/IntelliqDevops/maven.git'
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
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: '16a33b55-c049-433e-b885-6d661086cbe1', path: '', url: 'http://172.31.11.108:8080')], contextPath: 'test', war: '**/*.war'
            }
        }
        stage('continousTesting')
        {
            steps{
                git 'https://github.com/IntelliqDevops/FunctionalTesting.git'
                sh 'java -jar /home/ubuntu/.jenkins/workspace/declarativepipeline3/testing.jar'
            }
        }
        stage('continousDelivery')
        {
            steps{
                input message:'waiting for approval from the DM',submitter:'sahana'
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: '07266d3a-1612-4c4d-b84a-9da1fb868748', path: '', url: 'http://172.31.13.125:8080')], contextPath: 'prod', war: '**/*.war'
            }
        }
    }
}
