pipeline
{
    agent any
    stages
    {
        stage('continuousDownload')
        {
            steps
            {
                git 'https://github.com/gassama85/maven.git'
            }
        }
        stage('continuousBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('continuousDeployment')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: 'da254cad-be88-4217-b6fb-2307247462ca', path: '', url: 'http://172.31.95.156:8080')], contextPath: 'testapp', war: '**/*.war'
            }
        }
        stage('continuousTesting')
        {
            steps
            {
                git 'https://github.com/gassama85/FunctionalTesting.git'
                sh 'java -jar /home/ubuntu/.jenkins/workspace/DeclarativePipeline/testing.jar'
            }
        }
       
    }
    post
    {
        success
        {
             deploy adapters: [tomcat9(credentialsId: 'da254cad-be88-4217-b6fb-2307247462ca', path: '', url: 'http://172.31.85.232:8080')], contextPath: 'prodapp', war: '**/*.war'
        }
        failure
        {
            mail bcc: '', body: 'Jenkins had failed in CI ', cc: 'gassama85@yahoo.com', from: '', replyTo: '', subject: 'CI failure notice', to: 'gassama85@gmail.com'
        }
    }
}
