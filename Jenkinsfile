pipeline
{
    agent any
    stages
    {
        stage ('down')
        {
            steps
            {
            git 'https://github.com/IntelliqDevops/maven.git'    
            }
        }
        stage ('build')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('deploy')
        {
            steps
            {
            deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: '2d515b98-d9f3-4b20-baa0-986954636511', path: '', url: 'http://172.31.2.5:8080')], contextPath: 't', war: '**/*.war'
            }
        }
        stage('test')
        {
            steps
            {
                 git 'https://github.com/IntelliqDevops/FunctionalTesting.git'
                 sh 'java -jar /var/lib/jenkins/workspace/Development/testing.jar'
            }
        }
        stage ('delivery')
        {
            steps
            {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: '2d515b98-d9f3-4b20-baa0-986954636511', path: '', url: 'http://172.31.11.78:8080')], contextPath: 'p', war: '**/*.war'
            }
        }
    }
    
}

