pipeline {
    agent any 

    stages {
        stage('Build') { 
            steps { 
                sh 'mvn clean -DskipTests package -U' 
            }
        }
        stage('Test'){
            steps {
                sh 'mvn test pmd:pmd pmd:cpd' 
            }
        }
        stage('Deploy') {
            steps {
                sh 'echo "No docker, no cry ;)"'
            }
        }
    }
    post {
        always {
            junit 'target/surefire-reports/*.xml' 
            recordIssues enabledForFailure: true, tools: [mavenConsole(), java(), javaDoc()]
            recordIssues enabledForFailure: true, tool: cpd(pattern: '**/target/cpd.xml')
            recordIssues enabledForFailure: true, tool: pmdParser(pattern: '**/target/pmd.xml')
            archiveArtifact 'target/*.jar'
        }
    }
}
