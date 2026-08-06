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
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: '18e38879-a883-40a3-8276-8103a0e6d18d', path: '', url: 'http://172.31.0.190:8080')], contextPath: 'testapp', war: '**/*.war'
            }
        }
        stage('continousTesting')
        {
            steps{
                git 'https://github.com/IntelliqDevops/FunctionalTesting.git'
                sh 'java -jar /home/ubuntu/.jenkins/workspace/dock/testing.jar'
            }
        }
        stage('continousDelivery')
        {
            steps{
                input message:'waiting for approval from the DM',submitter:'sahana'
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: '64777c23-8523-45ec-afcb-2ec08b6d2d19', path: '', url: 'http://172.31.14.111:8080')], contextPath: 'prodapp', war: '**/*.war'
            }
        }
    }
}
