pipeline
{
    agent any
    stages
    {
        stage('continuousDownload')
        {
            steps
            {
                git 'https://github.com/gassama85/Jenkinsfile5.git'
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
                deploy adapters: [tomcat9(credentialsId: '8282fc14-5abb-4587-989d-a20a114d2ed3', path: '', url: 'http://172.31.16.56:8080')], contextPath: 'testapp', war: '**/*.war'
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
             deploy adapters: [tomcat9(credentialsId: '8282fc14-5abb-4587-989d-a20a114d2ed3', path: '', url: 'http://172.31.17.201:8080')], contextPath: 'prodapp', war: '**/*.war'
        }
        failure
        {
            mail bcc: '', body: 'Jenkins had failed in CI ', cc: 'gassama85@yahoo.com', from: '', replyTo: '', subject: 'CI failure notice', to: 'gassama85@gmail.com'
        }
    }
}
