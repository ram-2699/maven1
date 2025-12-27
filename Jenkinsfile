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
            deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: '8f15884a-6b4c-48e1-b5f5-a4a86b7328d1', path: '', url: 'http://172.31.15.223:8080')], contextPath: 'tee', war: '**/*.war'
            }
        }
        stage('test')
        {
            steps
            {
                 git 'https://github.com/IntelliqDevops/FunctionalTesting.git'
                 sh 'java -jar /var/lib/jenkins/workspace/slow/testing.jar'
            }
        }
        stage ('delivery')
        {
            steps
            {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: '8f15884a-6b4c-48e1-b5f5-a4a86b7328d1', path: '', url: 'http://172.31.14.144:8080')], contextPath: 'pee', war: '**/*.war'
            }
        }
    }
    
}

