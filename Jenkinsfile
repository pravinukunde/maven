pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/maven.git'
            }
        }
        stage('ContinuousBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('ContinuousDeployment')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '75818509-8dab-4b4d-b770-3a779abc2b08', path: '', url: 'http://172.31.94.77:8080')], contextPath: 'testapp', war: '**/*.war'
            }
        }
        stage('ContinuousTesting')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar  /var/lib/jenkins/workspace/DeclarativePipeline/testing.jar'
            }
        }
        stage('ContinuosuDelivery')
        {
            steps
            {
              input message: 'Need permission to continue', submitter: 'jay'
              deploy adapters: [tomcat9(credentialsId: '75818509-8dab-4b4d-b770-3a779abc2b08', path: '', url: 'http://172.31.81.12:8080')], contextPath: 'prodapp', war: '**/*.war'
            }
        }
        
        
        
    }
}

