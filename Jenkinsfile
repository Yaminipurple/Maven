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
              sh ' mvn package'
            }
        }
        stage('ContinuousDeployment')
        {
            steps
            {
              deploy adapters: [tomcat9(credentialsId: '36339f51-9886-4ecf-b238-330673790c6f', path: '', url: 'http://172.31.17.140:8080')], contextPath: 'mytestapp', war: '**/*.war'
            }
        }
        stage('ContinuousTesting')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline/testing.jar'
            }
        }
        stage('ContinuousDelivery')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '36339f51-9886-4ecf-b238-330673790c6f', path: '', url: 'http://172.31.22.185:8080')], contextPath: 'myprodapp', war: '**/*.war'
            }
        }
    }
}
