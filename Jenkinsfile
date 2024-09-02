pipeline{
    agent any
    
    stages{
        stage("checkout"){
            steps
            {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/2-alex/course3-jenkins-gs-spring-petclinic']])
            }
        }
        stage("build")
        {
            steps
            {
                sh './mvnw package'
            }
        }
    
        stage("publish")
        {
            steps{
                archiveArtifacts artifacts: '**/target/*.jar', followSymlinks: false
                recordCoverage(tools: [[parser: 'JACOCO']])
                junit stdioRetention: '', testResults: '**/target/surefire-reports/TEST*.xml'
            }
        }    
    }
    post
    {
        always
        {
            print ("${currentBuild.currentResult}")// add emailing code here
        }
    }
}
